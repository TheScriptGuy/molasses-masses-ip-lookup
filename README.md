# ip_lookup

`ip_lookup` is a fast, standalone command-line tool written in C that determines whether a given IP address or subnet is contained in a custom binary database. The database is encoded using a prefix trie and optionally encrypted using AES-256-ECB. This tool supports both IPv4 and IPv6 lookups.

## Features

- ⚡ Ultra-fast lookup using memory-mapped binary files
- 🔐 Optional AES-256 decryption with password
- ✅ Verifies SHA256 hash and 30-day freshness of the database
- 📦 Small binary, dynamically linked with OpenSSL

## Required Libraries

The following libraries must be installed on your system to compile and run `ip_lookup`:

### Runtime

- **OpenSSL** (dynamic)
  - Provides:
    - `libssl.so` / `libssl.dylib`
    - `libcrypto.so` / `libcrypto.dylib`
  - Used for:
    - AES-256 decryption via EVP
    - SHA256 hashing

### Installation Instructions

#### Debian/Ubuntu:

```bash
sudo apt update
sudo apt install libssl-dev pkg-config
```

## Usage

```bash
ip_lookup --input <db_file> --ip <ip_address> [options]
```

## Required Arguments

`--input <db_file>`
Path to the .bin database file to search.

`--ip <ip_address>`
The IPv4 or IPv6 address to check. The tool will determine if this IP is contained within the prefix trie embedded in the database.

## Optional Arguments

`--password <aes_key>`
If the database is encrypted, provide a decryption key (max 32 bytes). If this is omitted and encryption is required, the tool will fail.

## Output

`True` if the IP address exists in the database

`False` otherwise

## Example

```bash
ip_lookup --input embargo-v4.db --ip 192.0.2.1
```
