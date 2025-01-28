Hi Braden,

I was referred to you by my manager, Mike McGrail. I've been working extensively with Windows Event Logs (WEL) for various customers, and Abbott is currently a priority. They have requested to log-aggregate all WEL for compliance retention, which doesn't seem feasible with our current Enterprise Agent (EA) offering. Specifically, they want to retain Sysmon and PowerShell events.

I've encountered several challenges with our offering on both customer and non-customer SentinelOne (S1) tenants. Despite testing many policy override permutations, capturing the System channel events has been particularly difficult. For example, with the following configuration, I managed to get Application, Security, and Sysmon events, but System events were sparse:

```json
{
  "deepVisibility": {
    "eventLog": {
      "channels": {
        "Application": [],
        "ForwardedEvents": [],
        "Microsoft-Windows-Sysmon/Operational": [],
        "Security": [],
        "Setup": [],
        "System": [],
        "Windows PowerShell": []
      },
      "levels": [],
      "sendOriginalXML": true
    }
  }
}
```

After clearing the system logs in the event viewer and starting over, I finally saw some System events, but the process has been inconsistent. I understand that defining specific event IDs limits the total to 23 per channel, which complicates comprehensive logging.

Given Abbott's interest in retaining Sysmon and PowerShell events, could you help me compose the best configuration to capture as many events as possible? Additionally, it would be helpful to understand the limitations of this configuration, such as what might be excluded.

I also attempted to define around 422 channels in a policy override configuration, which initially seemed to work but eventually stopped reporting in the Singularity Data Lake (SDL) until I simplified the configuration and reloaded the agent logs. This test was conducted on an AWS EC2 instance with 8GB RAM.

Any guidance you can provide would be greatly appreciated.

Best regards,
Steve VanAllen
