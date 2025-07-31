## C4_brUH
a lightweight, extensible network scanning tool that leverages nmap, tcpdump, and netcat to discover + verify open ports, capture live traffic + generate CSV or HTML reports. It supports service fingerprinting + parallel port confirmation + custom BPF filters + promiscuous mode toggling + Docker-based deployment.

-------->features
a) scan with nmap using service version detection and optional scripts (-sC)
b) capture live packets for a specified duration with tcpdump, toggling promiscuous mode or using a custom BPF filter
c) confirm open ports in parallel using concurrent.futures and netcat
d) generate CSV or HTML reports summarizing scan results and confirmations
g) containerize the tool with Docker for consistent environments

Prerequisites
I. python 3.7 or higher
II. nmap
III. tcpdump
IV. netcat (nc)
V. sudo privileges for tcpdump captures
VI. pipenv or virtualenv (optional, but recommended)

installation
1) clone the repository

bash
2) git clone https://github.com/wifiknight45/C4_brUH.git
3) cd network-scanner
4) create and activate a virtual environment (optional)

bash
python3 -m venv venv
4a) source venv/bin/activate

5) install dependencies
bash
pip install -r requirements.txt


---------->usage

bash

./scanner.py <target> [options]
Arguments and options:

<target> IP address or hostname to scan

--ports comma-separated list of ports to scan (default: 21,22,23,25,53,80,110,135,139,1433,1723,3306,3389,5900,6346,8080,8443,20034)

--scripts enable nmap service fingerprinting scripts (-sC)

--duration tcpdump capture duration in seconds (default: 30)

--no-promisc disable promiscuous mode in tcpdump

--filter <expression> custom BPF filter for tcpdump

--threads <n> maximum threads for parallel netcat checks (default: 10)

--report-format <csv|html> generate a report in CSV or HTML format

--report-file <path> output path for the report (defaults to scan_report.csv or scan_report.html)

---->examples
scan with default settings and generate CSV report

bash
./scanner.py 192.168.1.10 --report-format csv
run a deep fingerprint scan, capture for 60 seconds, and use a BPF filter

bash
./scanner.py example.com \
  --scripts \
  --duration 60 \
  --filter "tcp port 80 or port 443" \
  --report-format html \
  --report-file web_scan.html
disable promiscuous mode and increase parallel checks

bash
./scanner.py 10.0.0.5 \
  --no-promisc \
  --threads 20 \
  --report-format csv

----->Docker
1) build the Docker image

bash
2) docker build -t network-scanner .
3) run inside a container (grant capabilities for packet capture)

bash
docker run --rm \
  --net host \
  --cap-add NET_RAW \
  --cap-add NET_ADMIN \
  C4_brUH \
  192.168.1.0/24 \
  --report-format html

----------->project structure
scanner.py main script containing scan, capture, confirmation, and reporting logic
requirements.txt Python dependencies (xmltodict)
Dockerfile instructions to build a container image

Contributing
a) fork the repository
b) create a feature branch
c) implement your changes and add tests
d) submit a pull request

License
This project is licensed under the MIT License. See the LICENSE file for details.

---

Developer 
@wifiknight45
wifiknight45@proton.me
feel free to reach out with questions or feedback 
