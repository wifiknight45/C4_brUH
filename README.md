# C4_brUH

A Python-based network reconnaissance tool that integrates nmap, tcpdump, and netcat to perform port scanning, traffic capture, and port verification against a given target IP or hostname. Developed by @wifiknight45.

---

Table of Contents

1. Features
2. Requirements
3. Installation
4. Usage
5. Example Output
6. How It Works
7. Contributing
8. License
9. Author


---

Features

• Scans for the 20 most commonly vulnerable ports using Nmap
• Parses XML output from Nmap into JSON for easy analysis
• Captures live network traffic with tcpdump for 30 seconds
• Verifies truly open ports with Netcat
• Graceful error handling and timeout support


---

Requirements

• Python 3.6 or higher
• Nmap installed and in your `PATH`
• tcpdump installed and in your `PATH` (requires sudo privileges for packet capture)
• Netcat (`nc`) installed and in your `PATH`
• Python packages:• `xmltodict`



## You can install `xmltodict` via pip:

pip install xmltodict

OR
## for Jupyter Notebooks or goog colab:

!pip install xmltodict

---

Installation

1. Clone the repository:git clone https://github.com/wifiknight45/C4_brUH.git
2. Change into the project directory:cd C4_brUH
3. (Optional) Create and activate a virtual environment:python3 -m venv venv
source venv/bin/activate
4. Install the required Python dependencies:pip install -r requirements.txt


---

Usage

Make sure you have the required tools installed and accessible, then run:

./C4_brUH.py <target>

Replace `<target>` with an IP address or hostname. For example:

./C4_brUH.py 192.168.1.100

Command-Line Options

• `target`
The IP address or hostname to scan.


No additional flags are required—everything is automated once you provide the target.

---

Example Output

$ ./C4_brUH.py example.com

Nmap Scan Results:
  - Port: 21, State: closed, Service: ftp
  - Port: 22, State: open, Service: ssh
  - Port: 80, State: open, Service: http
  - …

Traffic capture saved to: /tmp/example.com_capture.pcap

Netcat Port Confirmation:
  - Port 22 is confirmed open
  - Port 80 is confirmed open

---

How It Works

1. Tool Check
Verifies that `nmap`, `tcpdump`, and `nc` are installed by running `which` on each.
2. Nmap Scan
Executes:nmap -sV -Pn -p 21,22,23,25,…,8443,20034 <target> -oX -Parses the XML output with `xmltodict` into JSON.
3. Traffic Capture
Runs:sudo tcpdump -i any host <target> -w /tmp/<target>_capture.pcap -G 30 -W 1Captures 30 seconds of packets to/from the target.
4. Port Verification
Iterates over discovered open ports and runs:nc -z -v -w5 <target> <port>Logs only the ports that successfully connect.


---

Contributing

Contributions, issues, and feature requests are welcome! Feel free to fork the repository and submit a pull request.

1. Fork this repository
2. Create your feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m 'Add some feature'`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a Pull Request


---

License

This project is licensed under the MIT License. See the LICENSE file for details.

---

Author

Created by @wifiknight45
wifiknight45@proton.me
Feel free to reach out with questions or feedback!
