# Sophos Firewall Updates

## Sophos FW Updates 1 - Trigger: Load All Sophos Clients

This workflow loads the managing org's Sophos clients and passes them to part 2.

## Sophos FW Updates 2 - Create Sophos FW Update Tickets

This workflow compares the loaded client with an exclusion template. It creates a ticket in CWM for the client. 
A each Sophos firewall in the client has it's firmware checked. If an update is not required, the ticket is closed.
If an update is needed, a change request note is added to the ticket and the ticket is escalated.

## Schedule Sophos Updates 3 - Pod

A trigger is needed for CWM ticket saved. Once the ticket has been processed by Change Request, a pod is added to the ticket for scheduling. If custom scheduling is needed, a link to a form is added as a ticket note. This workflow logs the firewall, firmware and schedule for updating in a template (since moved to Cosmos DB).

## Schedule Sophos Updates 4

This actually does the scheduling of the update through the Sophos API

## Check Sophos Update Schedule and Alert

This workflow runs hourly and queries the Cosmos DB to check if any firewalls have updated. If they have, it checks the firmware to confirm the update was successful and updates the ticket.
This also checks to see if any firewall are updating within the next hour. If so, a Teams notification is sent.
