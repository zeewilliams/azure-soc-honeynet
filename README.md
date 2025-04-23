# ☁️ Simulated SOC & Honeynet – Azure Lab

![null](images/soc-lab-cover.png) <!-- Replace with a cover image -->

---

## 📘 Introduction

In this lab, I built a simulated Security Operations Center (SOC) environment in Microsoft Azure. The setup includes honeypot systems to attract malicious behavior and Microsoft Sentinel for real-time monitoring and detection. This project mirrors the detection pipeline of a real SOC and helps develop cloud security and KQL (Kusto Query Language) skills.

---

## 🎯 Objectives

- Deploy virtual machines to simulate an enterprise environment
- Create a honeynet to detect attacker behavior
- Ingest logs into Microsoft Sentinel
- Write KQL queries and alerts to identify suspicious activity

---

## 🧰 Tools & Services Used

| Service/Tool          | Purpose                                     |
|------------------------|---------------------------------------------|
| Microsoft Azure        | Cloud infrastructure for the SOC            |
| Microsoft Sentinel     | SIEM platform for log ingestion and alerting|
| Log Analytics Workspace| Data connector for Sentinel                 |
| Kusto Query Language   | Custom queries for log analysis             |
| Windows Server + Client| VMs to simulate real infrastructure         |

---

## 🧪 Lab Walkthrough

### ✅ Step 1: Create Azure Resources

- Launch Azure portal
- Deploy the following:
  - 1x Windows Server (acts as Domain Controller or vulnerable target)
  - 1x Windows 10 Client (user simulation)
- Create a **Log Analytics Workspace**
- Enable **Microsoft Sentinel** on the workspace

---

### ✅ Step 2: Enable Data Connectors

- From Sentinel, open **Data Connectors**
- Enable the following:
  - Security Events (for Windows logs)
  - Azure Activity
  - Sysmon (optional for endpoint telemetry)

---

### ✅ Step 3: Simulate Attacker Activity

You can simulate attacks manually or use a tool like:

```powershell
Invoke-WebRequest -Uri https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1059.001/T1059.001.md -OutFile script.ps1
.\script.ps1
```

- Run suspicious PowerShell commands
- Trigger failed logins or port scans
- Observe changes from the honeypot

---

### ✅ Step 4: Create KQL Queries & Alerts

In Microsoft Sentinel, use the **Logs** pane and write KQL:

```kql
SecurityEvent
| where EventID == 4625
| summarize count() by Account, Computer, bin(TimeGenerated, 1h)
```

> Create alerts from these queries to simulate SOC Tier 1 workflow.

---

## 📸 Screenshots

| Description                     | Screenshot Placeholder              |
|---------------------------------|-------------------------------------|
| Sentinel Dashboard              | ![null](images/soc-sentinel.png)    |
| KQL Query Results               | ![null](images/soc-kql.png)         |
| Simulated Attack Logs           | ![null](images/soc-attack.png)      |

> Upload images to the `images/` folder and update the placeholders above.

---

## ✅ Key Takeaways

- 🛠️ Built an end-to-end SOC in Microsoft Azure  
- 🧪 Used honeypots to simulate attacker activity  
- 🧠 Gained hands-on experience with KQL and Sentinel alerts  
- 🚨 Practiced SIEM-based detection workflows  

---

## 📎 References

- [Microsoft Sentinel Documentation](https://learn.microsoft.com/en-us/azure/sentinel/)
- [Kusto Query Language Docs](https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/)
- [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)

---

## 📬 About Me

👋 I'm **Zee**, a cybersecurity analyst developing hands-on experience with enterprise cloud defense, incident detection, and SOC tooling. This lab helped build my cloud SIEM skills in a realistic simulated environment.

🔗 [Connect with me on LinkedIn](https://www.linkedin.com/in/zee-williams)  
🔍 [Explore more projects on GitHub](https://github.com/zeewilliams)
```
