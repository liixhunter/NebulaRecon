
---

```markdown
# 🔎 Subdomain Scanner Tool

A unified script for subdomain enumeration that combines multiple tools:
- **Assetfinder**
- **Subfinder**
- **Sublist3r**
- **AS3NT (Another Subdomain ENumeration Tool)**

It supports:
- Verbose mode with execution times and loading bars
- Error handling
- Saving results in either a single merged file or separate files per tool
- Deduplication of results
- Automatic extraction of subdomains from AS3NT CSV output

---

## 📦 Requirements

### 1. System Packages
Make sure your system has the following installed:

- `git`
- `golang`
- `python3` (tested with Python 3.10+; Python 3.13 also works)
- `python3-pip`
- `build-essential`
- `automake`
- `autoconf`
- `libtool`
- `pkg-config`
- `curl`
- `wget`
- `unzip`

Install on Debian/Ubuntu:
```bash
sudo apt update && sudo apt install -y git golang python3 python3-pip build-essential automake autoconf libtool pkg-config curl wget unzip
```

---

### 2. Go-Based Tools
Install via `go install` (ensure `$GOPATH/bin` is in your PATH):

```bash
go install github.com/tomnomnom/assetfinder@latest
go install github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
```

---

### 3. Python-Based Tools
Install with pip:

```bash
pip3 install sublist3r
```

---

### 4. AS3NT
AS3NT is a Python package. Install it with:

```bash
pip3 install as3nt
```

#### Required Python Modules
AS3NT depends on several modules. At minimum:

```bash
pip3 install shodan requests
```

If you see errors about missing modules, install them with pip as indicated.  
For example:
- `pip3 install shodan` → required for Shodan integration (`-sh` flag).
- `pip3 install ipwhois` → required for ASN lookups (`-as` flag).
- `pip3 install dnspython` → required for DNS queries.

---

### 5. Optional: Libpostal (if you use Amass)
If you ever switch back to Amass, you’ll need **libpostal**:

```bash
git clone https://github.com/openvenues/libpostal
cd libpostal
./bootstrap.sh
./configure
make
sudo make install
sudo make install-data
```

---

## 🚀 Usage

Run the script with either a single domain or a file of domains:

### Single Domain
```bash
./subscan.sh --url example.com --verbose
```

### File of Domains
```bash
./subscan.sh --file domains.txt
```

You will be prompted to choose:
- `single` → save all results into one merged file
- `separate` → save results into individual files per tool

---

## 📂 Output

- **Single mode**: one merged file (deduplicated)
- **Separate mode**: files per tool:
  - `<domain>_assetfinder.txt`
  - `<domain>_subfinder.txt`
  - `<domain>_sublist3r.txt`
  - `<domain>_as3nt.csv`
  - `<domain>_as3nt_subdomains.txt` (clean list extracted from CSV)

---

## ⚠️ Notes

- If AS3NT fails with `ModuleNotFoundError: No module named 'shodan'`, install the missing dependency:
  ```bash
  pip3 install shodan
  ```
- The script automatically extracts subdomains from AS3NT’s CSV output using:
  ```bash
  cut -d',' -f2 results.csv | sort -u > subdomains.txt
  ```
- Ensure `$GOPATH/bin` is in your PATH so Go tools can be executed:
  ```bash
  export PATH=$PATH:$(go env GOPATH)/bin
  ```

---

## 🎉 Done!

You’re ready to enumerate subdomains with a clean, unified tool.
```

---

✨ This README now covers **all requirements**: system packages, Go tools, Python tools, AS3NT, its dependencies, and optional libpostal.  

Would you like me to also generate a **requirements.txt** (for pip) and a **go.mod/go.sum** (for Go tools) so you can install everything with one command in each environment?

