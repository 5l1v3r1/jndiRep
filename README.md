# jndiRep - CVE-2021-44228
Basically a **bad** grep on even **worse** drugs.
- search for malicious strings
- decode payloads
- print results to stdout or file
- report ips (incl. logs) to AbuseIPDB

## Scanning
- Directory: `python3 jndiRep.py -d /path/to/directory`
- File: `python3 jndiRep.py -f /path/to/input.txt`
- Custom filter: `python3 jndiRep.py ... -g "ldap"`
- Threading: If scanning a directory, 4 threads will work on the files in parallel. You can change this by using `-t <threads>`.

## Output
You can either print results to a file or to stdout (includes coloring of IPs and payloads).
- stdout: `python3 jndiRep.py ...`
- file: `python3 jndiRep.py ... -o /path/to/output.txt`

## Reporting
For reporting, an API Key (hex string of length 80) for AbuseIPDB is required, which you can obtain by register at the service and request IP Reporting ability.

- Report IPs once: `python3 jndiRep.py ... -a <api key>`
- Report every occurrence: `python3 jndiRep.py ... -a <api key> --no-dedup`
- Change default comment: `python3 jndiRep.py ... -c "your custom comment"`
- Include logs: `python3 jndiRep.py ... --include-logs`

**Warning**: Reporting is provided "as is". PII will not be cut, decoded payloads will not be uploaded.

## Issues
- Create pull request with your solution
- Open an issue [here](https://github.com/js-on/jndiRep/issues) and I'll try to fix it asap

## Help
```
usage: jndiRep.py [-h] [-a API_KEY] [-d DIRECTORY] [-f FILE] [-g GREP] [-o OUTPUT] [-t THREADS] [-r] [-c COMMENT] [--include-logs] [--no-dedup]

optional arguments:
  -h, --help            show this help message and exit
  -a API_KEY, --api-key API_KEY
                        AbuseIPDB Api Key
  -d DIRECTORY, --directory DIRECTORY
                        Directory to scan
  -f FILE, --file FILE  File to scan
  -g GREP, --grep GREP  Custom word to grep for
  -o OUTPUT, --output OUTPUT
                        File to store results. stdout if not set
  -t THREADS, --threads THREADS
                        Number of threads to start. Default is 4
  -r, --report          Report IPs to AbuseIPDB with category 21 (malicious web request)
  -c COMMENT, --comment COMMENT
                        Comment sent with your report
  --include-logs        Include logs in your report. PII will NOT be stripped of!!!
  --no-dedup            If set, report ever occurrence of IP. Default: Report only once.
```