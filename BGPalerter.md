# BGPalerter

NTT  developed  it  for  monitoring prefixes:

 - hijacks,  visibility loss,  unexpected changes of  configuration 
 - We  released  it  open-source  (BSD-3-Clause)    
   https://github.com/nttgin/BGPalerter 
  - It  works  in real time 
  - It’s easy  to  use 
  - Includes auto configuration 
  - No  data collection needed

Self-configuring BGP monitoring tool, which allows you to monitor in  **real-time**  if:

-   any of your prefixes loses visibility;
-   any of your prefixes is hijacked;
-   your AS is announcing RPKI invalid prefixes (e.g., not matching prefix length);
-   your AS is announcing prefixes not covered by ROAs;
-   any of your ROAs is expiring;
-   ROAs covering your prefixes are no longer reachable;
-   RPKI Trust Anchors malfunctions;
-   a ROA involving any of your prefixes or ASes was deleted/added/edited;
-   your AS is announcing a new prefix that was never announced before;
-   an unexpected upstream (left-side) AS appears in an AS path;
-   an unexpected downstream (right-side) AS appears in an AS path;
-   one of the AS paths used to reach your prefix matches a specific condition defined by you.

### Download & Run

1.  Download the binary  [here](https://github.com/nttgin/BGPalerter/releases)  (be sure to select the one for your OS)
    
2.  Execute the binary (e.g.,  `chmod +x bgpalerter-linux-x64 && ./bgpalerter-linux-x64`)  
    The first time you run it, the auto-configuration will start.
    

If something happens (e.g., a hijack) you will see the alerts in  `logs/reports.log`. In  `config.yml`  you can find other reporting mechanisms (e.g., email, Slack, Kafka) in addition to logging on files. Uncomment the related section and configure according to your needs.

If the installation doesn't go smoothly, read  [here](https://github.com/nttgin/BGPalerter/blob/main/docs/installation.md). Read the documentation below for more options.

> If you are looking for a BGP and RPKI monitoring service based on BGPalerter, try  [PacketVis](https://packetvis.com/)

-- end.