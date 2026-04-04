# SOC Detection & Log Analysis Lab

Analyzed ~1.9M log events in **Splunk** using the **BOTS v3 dataset from GitHub**.

One IP stood out:

- Repeated access to `/member.php`
- 404s on `/favicon.ico` and `/robots.txt`
- User-agents didn’t fully align with normal traffic

Summary of activity:

- ~2800 requests
- 60+ unique paths
- Built a simple prioritization metric combining request volume and path diversity
- Identified patterns of abnormal activity (possible probing) while validating context

SOC Analyst Tier 1 workflow applied:

- Validate the activity
- Build detection for similar behavior
- Block or rate-limit traffic if confirmed suspicious

Still learning, but this lab helped me move beyond running queries to **actual investigative thinking**.

## Screenshots

See the `screenshots/` folder for visuals:

1. 01_IP_detection.png  
2. 02_member_php_endpoint.png  
3. 03_404_behavior.png  
4. 04_timechart_graph.png  
5. 05_user_agent_breakdown.png  
6. 06_risk_score.png
