<img width="1536" height="1024" alt="netsentinel" src="https://github.com/user-attachments/assets/3f0bee4c-e78e-4cdf-81a0-88c75857c31a" />
# NetSentinel
Network Security Monitoring and Rule-Based Risk Assessment Platform using Python, Nmap, Flask and SQLite

# NetSentinel
## Network Security Monitoring and Rule-Based Risk Assessment Platform

NetSentinel is a localhost-only training project built in Kali Linux with Python, Nmap, Flask and SQLite. It performs TCP service discovery against the local machine, displays results in a web dashboard, applies explainable rule-based observations, and stores scan history.

> **Scope and safety:** The current scanner intentionally permits loopback targets only (for example, `127.0.0.1`). Use scanning features only on systems you own or have explicit permission to assess.

## Features
- Nmap TCP connect scan with service/version detection (`-sT -sV -T3 -F`).
- Flask web dashboard and JSON scan endpoint.
- Loopback IP validation.
- Port, protocol, state, service and version display.
- Rule-based observations with severity, score, evidence and recommendations.
- SQLite scan history.

## Architecture
1. Browser submits a target to Flask `/api/scan`.
2. The app validates the IP and restricts the current training scope to loopback.
3. Nmap discovers selected TCP ports and attempts service/version identification.
4. Python risk rules evaluate open services.
5. Scan data is saved through the SQLite database manager.
6. JSON results update the dashboard; `/api/history` supplies recent scans.

See `docs/NetSentinel_Project_Documentation.pdf` for detailed technical documentation.

## Technology
Kali Linux · Python 3 · Nmap · python-nmap · Flask · SQLite · HTML · CSS · JavaScript

## Setup (Kali Linux)
```bash
sudo apt update
sudo apt install -y python3 python3-venv python3-pip nmap git
cd ~/Desktop/NetSentinel
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python app.py
```
Open `http://127.0.0.1:5000/` and scan `127.0.0.1`. Keep the Flask terminal open.

## API test
```bash
curl -sS -X POST http://127.0.0.1:5000/api/scan \
  -H "Content-Type: application/json" \
  -d '{"target":"127.0.0.1}' | python -m json.tool
```

## Example demonstration
One successful local scan identified TCP/80 (Apache), TCP/3306 (MariaDB/MySQL) and TCP/5000 (Werkzeug). The rules returned three INFO observations for that loopback scan. Your results may differ depending on running services.

## Risk interpretation
The risk engine is a small rule-based triage component. A detected open port is not automatically a vulnerability. Severity and score values are project-defined and are not CVSS ratings. The scanner does not validate exploitability.

## Limitations and safety
- Current target scope is loopback only.
- `-F` scans Nmap's fast-port list, not every port.
- Service/version detection can be incomplete or inaccurate.
- This is not a full vulnerability scanner or production monitoring system.
- Flask's development server/debug mode must not be exposed publicly. Use a production WSGI server and disable debug mode before any deployment.
- Never commit passwords, API keys, tokens, private scan data, local databases, backups or the virtual environment.

## Future work
Automated PDF reports from real scan data, persistent risk-assessment records, automated tests, stronger logging, authentication and deployment hardening.

## Portfolio summary
Built a localhost-only network monitoring and rule-based security assessment platform using Kali Linux, Python, Nmap, Flask and SQLite. Implemented service discovery, a web dashboard, explainable security observations and persistent scan history.

**Skills:** Python, Linux/Kali, Nmap, Flask, SQLite, TCP/IP, service enumeration, input validation, security triage and debugging.

## License
Choose a license before presenting the repository as open source. If you do not intend to grant reuse rights, keep the repository private or publish without a license after considering your goals.
