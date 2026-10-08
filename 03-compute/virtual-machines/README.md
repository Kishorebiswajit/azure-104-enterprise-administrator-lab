# Virtual Machines Implementation

This document records the Linux VM infrastructure actually deployed for the AZ-104 enterprise administrator lab.

## Compute resource group

All three VMs are deployed in:

`RG-AZ104-COMPUTE`

Region:

`Central India`

## VM inventory

| VM | Tier | OS | Size | Private IP | Primary workload |
| --- | --- | --- | --- | --- | --- |
| `VM-AZ104-Management` | Management | Ubuntu 24.04.4 LTS | Standard_B2ats_v2 | `10.10.0.4` | Administration / management |
| `VM-AZ104-Web` | Web | Ubuntu 24.04 LTS | Standard_B2ats_v2 | `10.10.1.4` | Nginx |
| `VM-AZ104-App` | App | Ubuntu 24.04 LTS | Standard_B2ats_v2 | `10.10.2.4` | Python application on TCP/8080 |

The app VM has no public IP in the final architecture.

## Management VM

`VM-AZ104-Management` is the administration tier.

It was used for:

- Azure/Linux administration.
- Private connectivity testing.
- SSH validation.
- Testing access to the app VM.
- Operational troubleshooting.

The management VM is connected to `snet-management`.

## Web VM

`VM-AZ104-Web` provides the web tier.

Nginx was installed and configured with a custom lab page showing:

- AZ-104 Enterprise Lab.
- Web Tier — `VM-AZ104-Web`.
- Private IP `10.10.1.4`.
- Nginx.
- Operational status.

Validation completed:

```text
curl -I http://10.10.1.4
HTTP 200
```

The web VM is connected to `snet-workload`.

A NAT Gateway was added to this subnet after outbound package operations initially timed out.

## App VM

`VM-AZ104-App` provides the application tier.

The application was created under:

```text
/opt/az104-app/app.py
```

The Python service listens on:

```text
0.0.0.0:8080
```

The service is managed by systemd:

```text
/etc/systemd/system/az104-app.service
```

Core service behavior:

- Runs as `azureadmin`.
- Starts automatically with the VM.
- Restarts automatically if the process exits.
- Uses `/opt/az104-app` as the working directory.

The final service state was active/running and enabled.

Local validation returned the App Tier page from:

```text
http://localhost:8080
```

## Application traffic validation

The intended application flow is:

```text
VM-AZ104-Web
      |
      | TCP 8080
      v
VM-AZ104-App
```

The Web → App TCP/8080 path was tested successfully.

Management → App TCP/22 was also tested successfully for private administration.

Web → App TCP/22 was intentionally not permitted by the app-tier NSG.

## Secure access

The final app tier does not require a public IP.

Administration was performed through:

- Azure Bastion.
- Private VNet connectivity from the management tier.

Bastion was deployed with the Developer SKU for the lab. The Developer SKU has a one-active-VM-connection limitation, which was observed during testing.

## Monitoring

Azure Monitor Agent was installed successfully on all three VMs.

DCR associations:

- `DCRA-Z104-Management`
- `DCRA-Z104-Web`
- `DCRA-Z104-App`

The DCR sends Linux performance and syslog data to `LAW-AZ104-Enterprise`.

## Operational considerations

- VM auto-shutdown was configured for the management VM at 19:00 IST to control lab cost.
- Public exposure was minimized by removing the app VM public IP.
- NSGs enforce tier-specific traffic requirements.
- NAT Gateway provides explicit outbound connectivity for the workload subnet.

## Validation checklist

| Test | Result |
| --- | --- |
| Management VM reachable | Passed |
| Web VM Nginx responds | Passed |
| Management → App TCP/22 | Passed |
| Web → App TCP/8080 | Passed |
| Web → App TCP/22 | Denied as intended |
| App service enabled | Passed |
| App service running | Passed |
| App VM public IP removed | Passed |
| AMA installed on all VMs | Passed |
