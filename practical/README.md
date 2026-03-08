# Practical

Here I am talking about my hands-on experience form practical stuff in my own head important courses.

## Cyber Security Exercise 1 — Building Blue Team Organizations from Scratch

- **Platform:** Proxmox (virtualized environment)
- **Scope:** Built two complete company infrastructures from the ground up
- **Role:** White team — responsible for building and maintaining the entire infrastructure
- **Collaboration:** Team exercise with coursemates as part of JAMK cybersecurity coursework

**Infrastructure built for each organization:**

**Networking & Security**
- Configured dedicated firewalls for each organization
- Designed and implemented network segmentation
- Set up intranet for internal communication

**Domain & Services**
- Deployed and configured domain controllers
- Set up internal mail services for each organization
- Established DNS and domain management

**Monitoring & Data**
- Deployed SIEM for log collection and monitoring (limited personal involvement)
- Set up PCAP for network traffic capture and analysis
- Built databases populated with mocked data to simulate a real production environment

**Kill Chain Scenario**
- Designed and executed an insider threat kill chain where an internal attacker modified database data
- Blue Team 1 and Blue Team 2 had to detect and respond to the attack independently

**Key Takeaways:**
- Gained experience building enterprise infrastructure from zero
- Learned how different services (firewall, mail, DC, SIEM) depend on and interact with each other
- Analyzed data to trace the insider threat through the kill chain
- Observed and evaluated how both blue teams detected and reacted to the same incident differently

## Cyber Security Exercise 2 — Red Team Campaign Against Blue Teams

- **Role:** Red team operator
- **Collaboration:** Joint exercise with YAMK (Master's degree) students
- **Scope:** Planned and executed attack campaigns against three separate blue teams

**Overview**
- Designed attack campaigns targeting three different blue team organizations
- Performed injections and exploited vulnerabilities across various systems and services
- Worked as part of a red team alongside more experienced YAMK students

**Key Takeaways:**
- Hands-on experience with real attack planning and execution
- Learned how to identify and exploit vulnerabilities in different systems
- Gained understanding of how attacks look from the offensive side, complementing the defensive experience from Exercise 1

