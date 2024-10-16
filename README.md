# john-the-ripper---cheatsheet
Here’s a detailed cheat sheet on John the Ripper that you can use

---

John the Ripper is a powerful and flexible password-cracking tool used for security testing and recovery. It supports multiple attack methods and various password hash types. Below is a comprehensive guide on how to use John the Ripper effectively.

---

## Installation

John the Ripper is pre-installed on many penetration testing distributions like Kali Linux. If it's not installed, you can install it using the following command:

```bash
sudo apt-get install john
```

---

## Basic Usage

### Cracking a Password Hash
To crack a password hash using John, simply provide the hash file:

```bash
john <hash_file>
```

John will automatically detect the hash type and begin the cracking process.

### Using a Custom Wordlist
By default, John uses a built-in wordlist, but you can specify a custom wordlist using the `--wordlist` option:

```bash
john --wordlist=/path/to/wordlist.txt <hash_file>
```

### Resume Cracking
If you need to pause John and continue later, use the following command to resume cracking:

```bash
john --restore
```

### Show Cracked Passwords
After cracking, view the cracked passwords with:

```bash
john --show <hash_file>
```

---

## Extracting Hashes

### ZIP File Hash Extraction
To crack a password-protected ZIP file, first extract the hash using `zip2john`:

```bash
zip2john protected.zip > hash.txt
```

Then, run John the Ripper:

```bash
john hash.txt
```

### PDF File Hash Extraction
For password-protected PDF files, use `pdf2john`:

```bash
pdf2john protected.pdf > hash.txt
```

Then crack the hash:

```bash
john hash.txt
```

### RAR File Hash Extraction
For RAR files, use `rar2john`:

```bash
rar2john protected.rar > hash.txt
```

Then proceed to crack the hash:

```bash
john hash.txt
```

---

## Attack Types

### Dictionary Attack
John uses a wordlist to attempt cracking the password:

```bash
john --wordlist=/path/to/wordlist.txt <hash_file>
```

### Brute Force Attack
For brute force attacks, John tries all possible combinations of characters:

```bash
john <hash_file>
```

### Incremental Attack
The incremental mode is an advanced brute-force attack with John’s built-in rules:

```bash
john --incremental <hash_file>
```

This mode can take a long time but may find more complex passwords.

---

## Hash Formats

John the Ripper supports a variety of hash formats. You can specify the hash format with the `--format` option. Some common formats include:

- **MD5**: `--format=raw-md5`
- **SHA-256**: `--format=raw-sha256`
- **NTLM**: `--format=nt`
- **bcrypt**: `--format=bcrypt`

Example:

```bash
john --format=raw-md5 <hash_file>
```

### Identifying Hash Types
If you're unsure of the hash type, you can use John to try detecting it:

```bash
john --format=auto <hash_file>
```

---

## Additional Options

- **Custom Rules**: Use the `--rules` option to apply password transformation rules (e.g., adding uppercase letters, numbers).
  
  ```bash
  john --rules --wordlist=/path/to/wordlist.txt <hash_file>
  ```

- **Saving Progress**: John saves its progress automatically. Use the `--restore` option to continue from where you left off.

- **Performance Optimization**: Use `--fork` to distribute the cracking task across multiple CPU cores:
  
  ```bash
  john --fork=4 <hash_file>
  ```

- **Session Management**: You can save and restore specific sessions for long cracking operations:
  
  ```bash
  john --session=mySession <hash_file>
  john --restore=mySession
  ```

---

## Cracking Example: ZIP File

1. Extract the hash from a password-protected ZIP file:

   ```bash
   zip2john secret.zip > secret_hash.txt
   ```

2. Use a wordlist attack to crack the password:

   ```bash
   john --wordlist=/usr/share/wordlists/rockyou.txt secret_hash.txt
   ```

3. Once the password is cracked, display it:

   ```bash
   john --show secret_hash.txt
   ```

---

## Notes

- **John the Ripper** supports a wide variety of hash types and password-protected file formats.
- Password cracking time varies based on the complexity of the password and the attack method used.
- Always ensure ethical use of John the Ripper for testing and security purposes only.

---

## Disclaimer

This guide is for educational purposes only. Do not use John the Ripper or any other password-cracking tools for unauthorized or illegal activities. Always ensure you have permission to test the security of systems or files.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

## Contributing

Contributions are welcome! If you have suggestions for improvements, new features, or find bugs, please open an issue or submit a pull request on GitHub.

## Author
- OffialWebSite https://www.openwall.com/john/
- Documentation for Linux: https://www.kali.org/tools/john/
- C4rbo (https://github.com/C4rbo)
