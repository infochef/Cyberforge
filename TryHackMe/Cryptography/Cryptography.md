---
box: Cryptography
date: 2025-10-21
---

# Cryptography — Quick Note

**Date:** 2025-10-20

## Quick notes / lessons
- A **hash value** is a fixed-size string or characters that is computed by a hash function. A **hash function** takes an input of an arbitrary size and returns an output of fixed length, i.e., a hash value. We will cover various exciting and clever uses of hash functions and values in this room.
- There’s just one problem with this. What if two users have the same password? As a hash function will always turn the same input into the same output, you will store the same password hash for each user. That means if someone cracks that hash, they gain access to more than one account. It also means someone can create a Rainbow Table to break the hashes.
- A **Rainbow Table** is a lookup table of hashes to plaintexts, so you can quickly find out what password a user had just from the hash. A rainbow table trades the time to crack a hash for hard disk space, but it takes time to create. Here’s a quick example to get an idea of what a rainbow table looks like.
- **HMAC (Keyed-Hash Message Authentication Code)** is a type of message authentication code (MAC) that uses a cryptographic hash function in combination with a secret key to verify the authenticity and integrity of data.

	An HMAC can be used to ensure that the person who created the HMAC is who they say they are, i.e., authenticity is confirmed; moreover, it proves that the message hasn’t been modified or corrupted, i.e., integrity is maintained. This is achieved through the use of a secret key to prove authenticity and a hashing algorithm to produce a hash and prove integrity.
	
	The following steps give you a fair idea of how HMAC works.
	
	1. The secret key is padded to the block size of the hash function.
	2. The padded key is XORed with a constant (usually a block of zeros or ones).
	3. The message is hashed using the hash function with the XORed key.
	4. The result from Step 3 is then hashed again with the same hash function but using the padded key XORed with another constant.
	5. The final output is the HMAC value, typically a fixed-size string.
- ![[Pasted image 20251020180119.png]]
- **Hashing**, as already stated, is a process that takes input data and produces a hash value, a fixed-size string of characters, also referred to as digest. This hash value uniquely represents the data, and any change in the data, no matter how small, should lead to a change in the hash value. Hashing should not be confused with encryption or encoding; hashing is one-way, and you can’t reverse the process to get the original data.
- **Encoding** converts data from one form to another to make it compatible with a specific system. ASCII, UTF-8, UTF-16, UTF-32, ISO-8859-1, and Windows-1252 are valid encoding methods for the English language. Note that UTF-8, UTF-16, and UTF-32 are Unicode encodings, and they can represent characters from other languages, such as Arabic and Japanese.
- Only **encryption**, which we covered in the previous rooms, protects data confidentiality using a cryptographic cipher and a key. Encryption is reversible, provided we know the cipher and can access the key.
- John the Ripper is a well-known, well-loved, and versatile hash-cracking tool. It combines a fast cracking speed with an extraordinary range of compatible hash types.
- A hash is a way of taking a piece of data of any length and representing it in another fixed-length form. This process masks the original value of the data. The hash value is obtained by running the original data through a hashing algorithm. Many popular hashing algorithms exist, such as MD4, MD5, SHA1 and NTLM.
- ![[Pasted image 20251020182508.png]]
- ![[Pasted image 20251021174137.png]]
- ![[Pasted image 20251021181313.png]]
- ![[Pasted image 20251021182235.png]]
- ![[Pasted image 20251021183016.png]]
- ![[Pasted image 20251021183832.png]]


## Commands
- john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash_to_crack.txt
- john --format=[format] --wordlist=[path to wordlist] [path to file] [path to file]
	- - `--format=`: This is the flag to tell John that you’re giving it a hash of a specific format and to use the following format to crack it
	- `[format]`: The format that the hash is in
- john --wordlist=[path to wordlist] [path to file]  [path to file]
	- - `--wordlist=`: Specifies using wordlist mode, reading from the file that you supply in the provided path
	- `[path to wordlist]`: The path to the wordlist you’re using, as described in the previous task
- wget https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py 
	- python3 hash-id.py
- `unshadow local_passwd local_shadow > unshadowed.txt`
	- - `unshadow`: Invokes the unshadow tool
	- `[path to passwd]`: The file that contains the copy of the `/etc/passwd` file you’ve taken from the target machine
	- `[path to shadow]`: The file that contains the copy of the `/etc/shadow` file you’ve taken from the target machine
- john --single --format=[format] [path to file] [path_to_file]
	- - `--single`: This flag lets John know you want to use the single hash-cracking mode
	- `--format=[format]`: As always, it is vital to identify the proper format.
- zip2john [options]  [zip file] > [output file]
	- - `[options]`: Allows you to pass specific checksum options to `zip2john`; this shouldn’t often be necessary
	- `[zip file]`: The path to the Zip file you wish to get the hash of
	- `>`: This redirects the output from this command to another file
	- `[output file]`: This is the file that will store the output
- rar2john [rar file] > [output file]
	- - `rar2john`: Invokes the `rar2john` tool
	- `[rar file]`: The path to the RAR file you wish to get the hash of
	- `>`: This redirects the output of this command to another file
	- `[output file]`: This is the file that will store the output from the command
		
	
