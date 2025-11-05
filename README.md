Proxmark MIFARE Dump Analyzer
Advanced MATLAB tool for comprehensive analysis of MIFARE Classic card dumps from Proxmark3. Goes beyond basic access bit decoding to provide deep security analysis, vulnerability detection, and data extraction.
Show Image
Show Image

🔍 What It Does
This tool performs complete forensic analysis of MIFARE Classic dumps, extracting security keys, decoding permissions, detecting vulnerabilities, finding hidden data, and generating visual reports. Essential for security auditing, penetration testing, and RFID forensics.

✨ Key Features
🔐 Security Analysis

✅ Extracts all keys (Key A and Key B from all sectors)
✅ Decodes access bits (C1, C2, C3) with full permission interpretation
✅ Validates access bits - detects corrupted/invalid configurations
✅ Weak key detection - identifies default/factory keys (FFFFFFFFFFFF, A0A1A2A3A4A5, etc.)
✅ Security scoring - counts weak keys and invalid access bits

🆔 Card Identification

✅ UID decoder - extracts and decodes 4-byte UID
✅ Manufacturer detection - identifies card manufacturer from UID
✅ BCC validation - verifies checksum integrity
✅ Card type detection - identifies Mini/1K/4K cards automatically
✅ SAK & ATQA extraction - full card identification

🔎 Data Extraction

✅ ASCII string extraction - finds readable text embedded in card data
✅ Value block detection - identifies and decodes MIFARE value blocks
✅ Binary data visualization - heatmaps and entropy analysis
✅ Suspicious block flagging - detects all-zero or all-FF blocks

📊 Visualization & Reports

✅ Color-coded heatmaps - visual representation of card data
✅ Entropy analysis - identifies structured vs random data
✅ Sector comparison - diff two dumps side-by-side
✅ CSV export - export block matrices for further analysis
✅ Professional reports - detailed sector-by-sector breakdown

🔧 Flexibility

✅ Multiple formats - reads .bin, .txt, .hex, .eml, .dump, .imhex files
✅ Batch processing - analyze multiple dumps at once
✅ Drag-and-drop - just pass filenames as arguments
✅ Struct output - programmatic access to all extracted data


🚀 Quick Start
Basic Usage
matlabanalyze_proxmark_dump_claude_NEW

Select your Proxmark3 dump file when prompted
View instant comprehensive analysis

Command-Line Usage
matlab% Analyze single dump
analyze_proxmark_dump_claude_NEW('card_dump.bin')

% Compare two dumps
analyze_proxmark_dump_claude_NEW('dump1.bin', 'dump2.bin')

% Return structured data
sectors = analyze_proxmark_dump_claude_NEW('dump.bin', 'return_struct', true);

% Auto-export CSV
analyze_proxmark_dump_claude_NEW('dump.bin', 'csvout', 'C:\exports')

📋 Example Output
========================================
FILE 1: access_card.bin
========================================
Detected MIFARE Classic 1K (1024 bytes)

=== UID INFORMATION ===
UID: 04A1B2C3
UID Type: 4-byte UID (Single size)
Manufacturer: NXP Semiconductors
BCC: D7 (valid)
SAK: 08
ATQA: 00 04

========================================
EXTRACTED ASCII STRINGS (min 4 chars)
========================================
Sector  2, Block  8, Bytes  128- 143: "JOHN DOE"
Sector  5, Block 20, Bytes  320- 335: "2024-11-05"

========================================
VALUE BLOCKS DETECTED
========================================
Sector | Block | Value (signed) | Value (unsigned) | Address
-------|-------|----------------|------------------|--------
   4   |  16   |           1500 |             1500 | 0x04

========================================
DETAILED SECTOR-BY-SECTOR ANALYSIS
========================================

+--------------------------------------+
| SECTOR 00                            |
+--------------------------------------+
  UID: 04A1B2C3

  Block 0 [Data]:
    Bytes: 04 A1 B2 C3 D7 08 00 04 00 00 00 00 00 00 00 00
    ASCII: ................
    Permissions: R:AB W:AB I:AB D:AB

  Block 1 [Data]:
    Bytes: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
    ASCII: ................
    Permissions: R:AB W:AB I:AB D:AB

  Block 2 [Data]:
    Bytes: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
    ASCII: ................
    Permissions: R:AB W:AB I:AB D:AB

  Block 3 [Trailer]:
    KeyA:    FFFFFFFFFFFF [!WEAK KEY]
    C-bits:  FF 07 80 (hex)
             11111111 00000111 10000000 (binary)
             [Access bits valid]
    GP:      69
    KeyB:    FFFFFFFFFFFF [!WEAK KEY]

    Decoded C-bits per block:
      Block 0: (C1=0, C2=0, C3=0)
      Block 1: (C1=0, C2=0, C3=0)
      Block 2: (C1=0, C2=0, C3=0)
      Block 3: (C1=0, C2=0, C3=0)

    Permissions interpretation (per MIFARE Classic rules):
      Block 0: R:AB W:AB I:AB D:AB
      Block 1: R:AB W:AB I:AB D:AB
      Block 2: R:AB W:AB I:AB D:AB
      Block 3: KeyA:W[A] AC:W[A] KeyB:W[A]

========================================
SECURITY SUMMARY
========================================
Sectors with weak keys: 16 / 16
Sectors with invalid access bits: 0 / 16

Suspicious blocks (all 0x00 or 0xFF):
  Sector  1: blocks 4(0x00) 5(0x00) 6(0x00)
  Sector  3: blocks 12(0xFF) 13(0xFF)

🎯 Use Cases
🔒 Security Auditing

Identify weak or default keys across all sectors
Detect misconfigured access permissions
Find suspicious data patterns (wiped blocks, corruption)
Validate access bit integrity

🕵️ Forensic Analysis

Extract hidden ASCII strings (names, dates, serial numbers)
Recover value block data (balances, counters)
Analyze UID and manufacturer information
Compare dumps to detect modifications

🧪 Penetration Testing

Quick vulnerability assessment of RFID systems
Map card structure and permissions
Identify attack vectors (readable Key B, writable access bits)
Generate professional audit reports

📚 Research & Education

Learn MIFARE Classic structure hands-on
Visualize binary card data with heatmaps
Understand access bit encoding
Study entropy patterns in RFID data


📊 Visual Outputs
The tool generates multiple MATLAB figures:
1. Byte Heatmap

Color-coded visualization of all card data
Red overlay shows sector trailer locations
Quickly identify data patterns and anomalies

2. Per-Block Entropy Plot

Shannon entropy for each 16-byte block
Low entropy = structured/repeated data
High entropy = random/encrypted data
Flags suspicious all-zero or all-FF blocks

3. XOR Comparison (when comparing two dumps)

Visual diff showing changed bytes
Highlights modified sectors/blocks
Essential for tracking card modifications

4. Byte Histogram

Distribution of byte values in chosen block
Helps identify encoding patterns
Useful for detecting value blocks


🔍 Advanced Features
UID Decoding
Extracts complete UID information:

4-byte UID in hex format
Manufacturer identification (NXP, ST Micro, Infineon, etc.)
BCC (checksum) validation
Detection of magic cards and cascade tags
SAK (Select Acknowledge) byte
ATQA (Answer To Request) bytes

Value Block Detection
Automatically identifies MIFARE value blocks:

Validates proper value block format
Extracts signed 32-bit value
Shows address byte
Detects corrupted value blocks

ASCII String Extraction
Finds embedded text strings:

Minimum 4 characters
Shows sector/block location
Byte range indicators
Filters non-printable characters

Access Bit Validation
Verifies access bit integrity:

Checks proper inversion encoding
Detects bit corruption
Identifies invalid configurations
Shows specific validation errors


📁 Supported Formats
Binary Formats

.bin - Raw binary dump (most common from Proxmark3)
.dump - Generic binary dump

Text/Hex Formats

.txt - Plain text hex dump
.hex - Hex dump with optional line numbers
.eml - Email format (32 hex chars per line)
.imhex - ImHex pattern format

Format detection is automatic - the tool intelligently parses any format!

📋 Requirements

MATLAB R2019b or newer
No additional toolboxes required
Proxmark3 (for creating dumps) - not required for analysis


🎓 Understanding the Output
Weak Keys
The tool checks for common default keys:

FFFFFFFFFFFF - Factory default (most common)
A0A1A2A3A4A5 - Another common default
000000000000 - All zeros
D3F7D3F7D3F7 - MAD key

⚠️ If detected: Card is vulnerable to attacks
Access Bit Notation

R:AB = Read with Key A or B
W:A = Write with Key A only
I:-- = Increment never allowed
D:AB = Decrement with Key A or B

Suspicious Blocks

All 0x00 = Wiped block or empty sector
All 0xFF = Erased block or corruption
Low entropy = Repeated pattern or padding


🔬 Technical Details
Supported Card Types
TypeSizeSectorsAuto-DetectedMIFARE Classic Mini320 bytes5❌ (rare)MIFARE Classic 1K1024 bytes16✅MIFARE Classic 4K4096 bytes40✅
Sector Structure (1K/Mini)
Each sector = 64 bytes (4 blocks × 16 bytes):
Block 0-2: Data blocks (48 bytes)
Block 3:   Trailer (16 bytes)
  - Bytes 0-5:   Key A
  - Bytes 6-8:   Access bits
  - Byte 9:      GP byte
  - Bytes 10-15: Key B
Value Block Format
MIFARE value blocks store signed 32-bit integers:
Bytes 0-3:   Value (little-endian)
Bytes 4-7:   ~Value (inverted)
Bytes 8-11:  Value (repeated)
Bytes 12-15: Address + ~Address (repeated)

🤝 Contributing
Contributions welcome!
Ideas for improvement:

MIFARE Ultralight support
DESFire parsing (currently stubbed)
MAD (MIFARE Application Directory) decoder
NDEF record parsing
GUI interface
PDF report generation
Automatic vulnerability scoring


📜 License
MIT License - Free for personal and commercial use

⚠️ Legal Disclaimer
For authorized security testing and research only.
Only analyze cards that:

✅ You own personally
✅ You have explicit written permission to test
✅ Are used in legitimate security research

Unauthorized RFID analysis is illegal.

🔗 Related Tools

Proxmark3 - RFID Swiss Army Knife
libnfc - Low-level NFC library
mfoc - MIFARE Classic Offline Cracker
mfcuk - MIFARE Classic Universal toolKit


📧 Support

Issues: GitHub Issues for bugs and feature requests
Questions: GitHub Discussions
Security: Report privately via GitHub Security tab


⭐ Like This Tool?
If you find this analyzer useful:

⭐ Star the repository
🔄 Share with the security community
🐛 Report any bugs you find
💡 Suggest features you'd like
