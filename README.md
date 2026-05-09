# CyLab Security Academy Forensics Writeups

Welcome to my CyLab Security Academy Forensics Writeups repository.

This repository contains beginner-friendly solutions, commands, explanations, and scripts for various PicoCTF Forensics challenges.

---

# Challenges Included

1. Riddle Registry  
2. Hidden in Plain Sight  
3. Flag in Flame  
4. Corrupted File  
5. DISKO 1  
6. RED  
7. Verify  
8. Scan Surprise  
9. Secret of the Polyglot  
10. Can You See Me  
11. Information  
12. Glory of the Garden  
13. Binary Digits  
14. Ph4nt0m 1ntrud3r  

---

# 1. Riddle Registry

## Step 1: Extract metadata from the PDF

```bash
exiftool confidential.pdf
```

The flag is encoded in Base64 inside the `Author` section.

## Step 2: Decode the Base64 string

```python
import base64

data = input("Enter Base64 value: ")

decoded = base64.b64decode(data)

print(decoded.decode())
```

You can also use Linux:

```bash
echo b64string | base64 -d
```

---

# 2. Hidden in Plain Sight

## Step 1: Check the file type

```bash
file img.jpg
```

There is a Base64 encoded string in the comment section.

## Step 2: Decode the Base64 string

Use the same Python script from above.

The decoded output becomes:

```text
steghide:cEF6endvcmQ=
```

Decode the second Base64 string too.

You will get:

```text
pAzzword
```

## Step 3: Extract hidden data using Steghide

```bash
steghide extract -sf img.jpg
```

Enter the decoded password.

This extracts a `flag.txt` file containing the flag.

---

# 3. Flag in Flame

## Step 1: Decode the Base64 log file

```bash
base64 -d logs.txt > image.txt
```

## Step 2: Open the file

```bash
xdg-open image.txt
```

There is a hexadecimal string hidden in the image.

## Step 3: Decode the hex string

```python
data = input("Enter Hex data: ")

data_2 = bytes.fromhex(data)

txt = data_2.decode('utf-8')

print(txt)
```

---

# 4. Corrupted File

## Step 1: Check the file header

```bash
xxd -l 16 file
```

## Step 2: Create a copy of the file

```bash
cp file fixed.jpg
```

## Step 3: Edit the corrupted header

Change the `5c78` part of the header to `ffd8`.

Use:

```bash
hexedit fixed.jpg
```

## Step 4: Open the repaired image

```bash
xdg-open fixed.jpg
```

The flag is visible in the image.

---

# 5. DISKO 1

Run:

```bash
strings disko-1.dd | grep "picoCTF{"
```

This directly reveals the flag.

---

# 6. RED

## Step 1: Analyze the image

```bash
zsteg red.png
```

You will find a Base64 encoded string.

## Step 2: Decode the Base64 string

Use the Python script from Challenge 1.

You can also use:

```bash
echo b64string | base64 -d
```

---

# 7. Verify

After logging in as:

```text
tf-player@pico-chall$
```

## Step 1: Find the correct checksum

```bash
sha256sum files/* | grep "$(cat checksum.txt)"
```

This identifies the file with the correct checksum.

## Step 2: Run the decrypt script

```bash
./decrypt.sh files/file_name_with_correct_checksum
```

This reveals the flag.

---

# 8. Scan Surprise

Decode the QR code using:

```text
https://qrcoderaptor.com/
```

The decoded QR contains the flag.

---

# 9. Secret of the Polyglot

## Step 1: Inspect the file header

```bash
xxd flag2of2-final.pdf
```

The header reveals that the file is actually a PNG.

## Step 2: Convert the file extension

```bash
mv flag2of2-final.pdf flag2of2-final.png
```

## Step 3: Open both files

```bash
xdg-open flag2of2-final.pdf
```

```bash
xdg-open flag2of2-final.png
```

The flag is split into 2 parts between the PDF and PNG.

---

# 10. Can You See Me

## Step 1: Extract metadata

```bash
exiftool ukn_reality.jpg
```

There is a Base64 string in the `Attribution URL` section.

## Step 2: Decode the Base64 string

Use either:

- The Python script from Challenge 1
- Linux command:

```bash
echo b64string | base64 -d
```

---

# 11. Information

## Step 1: Extract metadata

```bash
exiftool cat.jpg
```

There is a Base64 string in the `License` section.

## Step 2: Decode the string

Use either:

```bash
echo b64string | base64 -d
```

or the Python script from Challenge 1.

---

# 12. Glory of the Garden

Run:

```bash
cat garden.jpg | grep -a "picoCTF{"
```

This directly reveals the flag.

---

# 13. Binary Digits

## Step 1: Use CyberChef

Paste the file contents into:

```text
https://cyberchef.io/
```

Use the `From Binary` operation.

## Step 2: Save the output

Download the resulting content as a JPG image.

The flag is hidden inside the image.

---

# 14. Ph4nt0m 1ntrud3r

## Step 1: Extract the Base64 packet data

Run:

```bash
tshark -r myNetworkTraffic.pcap -Y "tcp.len==12" -T fields -e tcp.segment_data | xxd -p -r | base64 -d
```

This automatically extracts the packet data, reconstructs the Base64 text in order, decodes it, and reveals the flag.

---

# Tools Used

- ExifTool
- Wireshark
- Tshark
- CyberChef
- Base64
- HexEdit
- xxd
- strings
- grep
- zsteg
- Steghide
- Python

---
# Tools Used

- ExifTool
- Wireshark
- CyberChef
- Base64
- HexEdit
- xxd
- strings
- grep
- zsteg
- Steghide
- Python

---

# Concepts Covered

- Metadata Analysis
- Base64 Decoding
- Hex Decoding
- Steganography
- File Header Repair
- QR Code Decoding
- PCAP Analysis
- Binary Data Extraction
- Image Forensics
- Hash Verification

---

# Disclaimer

This repository is for educational purposes only.
