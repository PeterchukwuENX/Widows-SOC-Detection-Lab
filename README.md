Windows SOC Investigation & Detection Lab

A Windows-based lab I'm building to actually practice the stuff a junior SOC analyst does day to day - watching endpoint activity, reading security events, and figuring out whether something's normal or worth flagging, using Windows' own tools plus Sysmon.

What this actually is

The idea is to simulate what a junior analyst would do if something suspicious showed up on a Windows machine - except I'm skipping the SIEM for now and going straight to the raw Windows telemetry first. I want to actually understand what's happening at the event-log level before leaning on a tool that summarizes it for me.

The investigation process, as I'm building it out:
1. Generate some controlled activity on the VM (logons, failed logons, processes, etc.)
2. Collect the resulting Windows and Sysmon logs
3. Pick out which events actually matter
4. Build a timeline of what happened, in order
5. Connect the dots - which process, which user, which command, at what time
6. Decide: does this look normal, or does it look like something worth escalating
7. Write it up
8. Say what I'd actually do about it

I'm building this one piece at a time on purpose - I'd rather actually understand each event as I hit it than memorize a list of Event IDs up front and hope it sticks.

What I'm trying to get good at
- Reading Windows security logs like they're actually telling a story, not just numbers
- Sysmon telemetry - the extra detail Windows' own logging doesn't give you
- Tracing a process back to whatever process launched it (parent-child relationships)
- Investigating PowerShell activity specifically, since that's a common place real attacks hide
- Authentication events - normal logons vs. failed ones
- RDP-specific investigation
- Spotting brute-force patterns
- Noticing when an account's behaving oddly
- Putting a timeline together from scattered log entries
- Actually documenting an investigation, not just solving it in my head
- The basics of detection engineering - writing rules that catch this stuff automatically

 The lab setup
Right now it's one Windows 10 VM running in VirtualBox on my host machine (8GB RAM allocated).
```text
                    HOST MACHINE
                 Windows 10 / 8 GB RAM
                         |
                     VirtualBox
                         |
                         v
              +-----------------------+
              |    WINDOWS SOC VM     |
              |                       |
              |     Windows 10        |
              |                       |
              |   +---------------+   |
              |   |    Sysmon     |   |
              |   +-------+-------+   |
              |           |           |
              |           v           |
              |    Windows Event      |
              |       Logs            |
              |           |           |
              |           v           |
              |    Event Viewer       |
              |           |           |
              |           v           |
              |   SOC Investigation   |
              +-----------------------+
```

## Why I'm building this

Part of my path toward a SOC analyst role. This is the Windows counterpart to the Linux hardening and log-review project I already did - same idea, different OS: generate something real, then go find it in the logs and reason through whether it matters.
