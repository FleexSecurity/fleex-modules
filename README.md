# Fleex Modules Repository

This repository contains a collection of YAML workflow modules for the Fleex distributed scanning tool.

## Usage

```bash
fleex scan -w module-name -n fleet-name -f fleet-name -i domains.txt -o results.txt
```

Override variables:
```bash
fleex scan -w module-name -n fleet-name -i domains.txt -o results.txt \
  --var RESOLVERS:/path/to/resolvers.txt
```

## Module Format

```yaml
name: tool-name
description: Brief description of what the module does
author: fleex

vars:                              # optional - custom variables
  WORDLIST: "/path/to/wordlist.txt"
  RESOLVERS: "/path/to/resolvers.txt"

files:                             # optional - files to transfer before execution
  - source: "{vars.WORDLIST}"
    destination: /tmp/wordlist.txt

setup:                             # optional - commands to run before steps
  - "apt-get update"

steps:                             # required - commands to execute
  - name: step-name
    command: "tool -i {INPUT} -o {OUTPUT}"
    timeout: "2h"                  # optional

output:
  aggregate: concat                # concat | sort-unique
  deduplicate: true                # remove duplicate lines
```

### Placeholders

| Placeholder | Description |
|-------------|-------------|
| `{INPUT}` | Input file (automatically chunked per box) |
| `{OUTPUT}` | Output file path |
| `{vars.KEY}` | Custom variable value |

## Available Modules

### Subdomain Enumeration

| Module | Description |
|--------|-------------|
| `subfinder` | Fast passive subdomain enumeration |
| `amass` | In-depth attack surface mapping |
| `assetfinder` | Find related domains and subdomains |
| `findomain` | Fast subdomain enumeration |
| `chaos-client` | Chaos DNS DB API client |
| `cero` | Scrape domains from SSL certificates |
| `github-subdomains` | Find subdomains from GitHub |
| `aiodnsbrute` | Async DNS brute-force |

### URL Discovery

| Module | Description |
|--------|-------------|
| `gau` | Fetch URLs from AlienVault, Wayback, CommonCrawl |
| `gauplus` | Enhanced gau with additional features |
| `waybackurls` | Fetch URLs from Wayback Machine |
| `github-endpoints` | Find endpoints from GitHub |

### DNS Tools

| Module | Description |
|--------|-------------|
| `dnsx` | Multi-purpose DNS toolkit |
| `puredns` | Fast domain resolver and bruteforcer |
| `massdns` | High-performance DNS resolver |
| `shuffledns` | Massdns wrapper for enumeration |
| `dnsgen` | Generate domain permutations |
| `dnsrecon` | DNS enumeration tool |
| `dnsvalidator` | Validate DNS resolvers |
| `dnscewl` | Generate target-specific DNS wordlist |
| `hakrevdns` | Reverse DNS lookup at scale |
| `dns-resolvers` | Fetch fresh resolvers from trickest |
| `six2dez-dns-permutations` | DNS permutation wordlist |

### HTTP Probing

| Module | Description |
|--------|-------------|
| `httpx` | Fast multi-purpose HTTP toolkit |
| `httprobe` | Probe for working HTTP/HTTPS servers |
| `tlsx` | Fast TLS grabber and analyzer |

### Directory/File Fuzzing

| Module | Description |
|--------|-------------|
| `ffuf` | Fast web fuzzer |
| `feroxbuster` | Recursive content discovery |
| `gobuster` | Directory enumeration |
| `dirdar` | File and directory search |
| `meg` | Fetch paths without hammering hosts |
| `kiterunner` | API endpoint discovery |

### Web Crawling

| Module | Description |
|--------|-------------|
| `gospider` | Fast web spider |
| `hakrawler` | Simple web crawler |
| `linkfinder` | Discover endpoints in JS files |
| `getjs` | Extract JavaScript files |
| `subjs` | Fetch JS files from URLs |
| `paramspider` | Mine parameters from Web Archives |
| `arjun` | HTTP parameter discovery |
| `fff` | Fast flexible fuzzer |
| `concurl` | Concurrent curl requests |
| `gorgo` | Fast web crawler |

### Vulnerability Scanning

| Module | Description |
|--------|-------------|
| `nuclei` | Template-based vulnerability scanner |
| `jaeles` | Web application scanner |
| `sqlmap` | SQL injection scanner |
| `dalfox` | XSS scanner |
| `commix` | Command injection tool |
| `gxss` | Check XSS payload acceptance |
| `kxss` | Check reflected parameters |
| `crlfuzz` | CRLF vulnerability scanner |
| `corsy` | CORS misconfiguration scanner |
| `openredirex` | Open redirect scanner |
| `subjack` | Subdomain takeover checker |
| `s3scanner` | AWS S3 bucket scanner |
| `wpscan` | WordPress security scanner |
| `testssl` | TLS/SSL testing |
| `trufflehog` | Credential leak finder |
| `erlpopper` | Erlang Port Mapper scanner |

### Port Scanning

| Module | Description |
|--------|-------------|
| `nmap` | Network exploration tool |
| `masscan` | Fast port scanner |
| `naabu` | Fast port scanner (Go) |
| `rustscan` | Modern fast port scanner |
| `unimap` | Scan hosts only once |

### Screenshots

| Module | Description |
|--------|-------------|
| `aquatone` | Visual inspection of websites |
| `gowitness` | Web screenshots with Chrome |
| `webscreenshot` | Take website screenshots |
| `scrying` | Web screenshot tool |

### Brute Force

| Module | Description |
|--------|-------------|
| `thc-hydra` | Network logon cracker |
| `medusa` | Parallel login brute-forcer |
| `crackmapexec` | Network pentesting swiss knife |

### Utilities

| Module | Description |
|--------|-------------|
| `anew` | Append unique lines to file |
| `gf` | Grep wrapper for patterns |
| `qsreplace` | Replace query string values |
| `anti-burl` | Check if URLs are alive |
| `exclude-cdn` | Exclude CDN IPs |
| `ipcdn` | Check CDN provider IPs |
| `leaky-paths` | Check common leaky paths |
| `interlace` | Run commands in parallel |
| `wafw00f` | WAF detection |

## Directory Structure

```
fleex-modules/
├── README.md
├── LICENSE
└── base_modules/
    ├── subfinder/
    │   └── module.yaml
    ├── amass/
    │   └── module.yaml
    ├── httpx/
    │   └── module.yaml
    └── ...
```

## Contributing

1. Fork the repository
2. Create a new module in `base_modules/your-tool/module.yaml`
3. Follow the module format above
4. Submit a pull request

> **Disclaimer**: These modules are provided for security research and educational purposes only, to help the cybersecurity community. The author assumes no responsibility for any misuse or damage caused by the improper use of these modules. Always ensure you have explicit authorization before testing any systems you do not own.

## License

Fleex modules is distributed under Apache-2.0 License
