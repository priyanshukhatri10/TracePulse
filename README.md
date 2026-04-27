# TracePulse
TracePulse is a high-performance Deep Packet Inspection (DPI) engine for offline network traffic analysis.  
It processes PCAP files, classifies traffic by application/domain using protocol parsing and TLS SNI extraction, and enforces blocking policies by IP, app, or domain using a multithreaded pipeline.
---
## Features
- Offline PCAP analysis (`.pcap`)
- Layered packet parsing (Ethernet, IPv4, TCP/UDP)
- Flow tracking using 5-tuple
- Application/domain classification via:
  - TLS SNI extraction
  - HTTP Host parsing
- Policy-based blocking:
  - `--block-ip`
  - `--block-app`
  - `--block-domain`
- Multithreaded processing architecture (Reader -> Load Balancers -> Fast Paths -> Writer)
- Detailed processing report:
  - total packets/bytes
  - forwarded vs dropped
  - app breakdown
  - thread statistics
  - detected SNIs/domains
---
## Project Structure
Packet_analyzer/
├── include/
├── src/
├── CMakeLists.txt
├── WINDOWS_SETUP.md
├── test_dpi.pcap
└── README.md
Build (Windows)
Option 1: Visual Studio (Developer Command Prompt)
Option 2: MinGW g++
Usage
Basic run
Block by app
Block by domain keyword
Block by source IP
Combined example
Example Output (Truncated)
How It Works (Workflow)
Read packets from input PCAP
Parse headers and payload metadata
Build/lookup flow state (5-tuple)
Extract SNI/Host and classify app/domain
Apply block rules (IP/App/Domain)
Forward allowed packets to output PCAP
Print final analytics report
Limitations
Offline analysis only (not live inline packet interception)
Encrypted payload content is not decrypted
Classification is signature/pattern based; some traffic remains Unknown
Domain blocking depends on visible SNI/Host metadata
Use Cases
Network traffic profiling and visibility
Policy testing on captured traffic
Educational DPI and protocol parsing experiments
Baseline architecture for advanced IDS/IPS research
Future Improvements
Expand app/domain signature database
Add persistent rule files (load/save rules)
Improve worker load distribution
Add QUIC/HTTP3-aware classification
Add live interface capture mode
License
Add your preferred license here (MIT/Apache-2.0/GPL, etc.).
