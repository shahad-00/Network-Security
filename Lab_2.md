# Lab 2: Hashing and File Integrity Verification

## Objectives

- Generate file checksums using MD5, SHA-1, and SHA-256.
- Compare calculated checksums with reference values.
- Observe matching and non-matching checksum results.
- Understand how hashing helps detect changes to file contents.

## Tools

- WinMD5Free
- Kali Linux Terminal
- sha1sum
- sha256sum
- md5sum
- grep

## Part 1 :
### Message Digest and Hashing functions

### EX1: Using MD5 to checksum file

- You are going to have a text file ( ex: Note , word document …etc )
- Add any text to the text file and save the file
- Compute the MD5 of the text and note the hash value V1
- Make a slight change to the text file and save the file
- Again, re-compute the MD5 of the text and note the hash value V2
- Now compare V1 and V2

### Practical Result

<img width="453" height="328" alt="Picture1" src="https://github.com/user-attachments/assets/7bb1ec36-d3c1-4f7e-8267-c801716dd6de" />


**Explanation:** WinMD5Free was used to calculate and compare MD5 checksums. The “NOT Matched!” message shows that the compared values differ.

This is consistent with a change to the file contents, although the screenshot itself does not show the editing step.

## Part2 :
### Message Authentication in Kali Linux

### To generate SHA1 checksum :

- Create a text file in your Desktop (ex: File2.txt)
- Add a text to the file (ex: this is the original message)
- Generate the sha1 checksum of the file
- shasum ~/Desktop/YourTextFile.txt
- sha1sum ~/Desktop/YourTextFile.txt

### To compare SHA1 checksum with a given one:

    sha1sum /path/to/file | grep <checksum>

First , change content of file then Generate the sha1 checksum of the file Again !!

After that use

    sha1sum ~/Desktop/File2.txt | grep <ADD The Given SHA1 Checksum Here>

### SHA-1: Matching Checksum

<img width="546" height="228" alt="Picture7" src="https://github.com/user-attachments/assets/9de2068d-354b-4c6d-92f1-553adb7ffe84" />


**Explanation:** The SHA-1 checksum of File2.txt was generated using:

    sha1sum ~/Desktop/File2.txt

The output was then filtered using grep with the matching reference checksum. The displayed line indicates that the reference value was found.

### SHA-1: Non-Matching Checksum

<img width="618" height="212" alt="Picture8" src="https://github.com/user-attachments/assets/4689547d-7d3a-4c2c-905e-3649a8aa8b84" />


**Explanation:** The SHA-1 output was compared with a different reference value. No matching line was displayed, indicating that the supplied value was not found in the output.

The screenshot demonstrates a non-match, but does not independently show that the file was edited.

### To generate SHA256 checksum:

Same commands for SHA256 checksums

<img width="640" height="329" alt="Picture9" src="https://github.com/user-attachments/assets/d27bd304-8a62-4dc8-b9d1-1d9ad68ea1c2" />


**Explanation:** The file’s SHA-256 checksum was generated using:

    sha256sum ~/Desktop/File2.txt

The output was compared with matching and non-matching reference values using grep. A matching value produced an output line, while the non-matching value produced no output.

### MD5 checksum:

Same commands for MD5 checksums

<img width="645" height="310" alt="Picture10" src="https://github.com/user-attachments/assets/8468a09e-5ed1-463a-ac67-8e4d9d7a9ac1" />


**Explanation:** The MD5 checksum was generated using:

    md5sum ~/Desktop/File2.txt

The screenshot shows comparisons against matching and non-matching values. The matching comparison displays the checksum line, while the non-matching comparison returns no line.

### Additional Checksum Practice

<img width="835" height="668" alt="Screenshot 2026-10-21 013537" src="https://github.com/user-attachments/assets/4e82261e-f06a-4cd1-8030-687a627adaf8" />


**Explanation:** Additional terminal practice shows checksum generation and comparisons for hacking.txt using SHA-1, SHA-256, and MD5.

### Understanding the Results

- A displayed matching line means grep found the supplied text in the checksum output.
- No output means grep did not find the supplied text.
- Red highlighting depends on terminal and grep settings; the color itself does not determine whether checksums match.
- A changed checksum indicates that the compared values differ. It does not identify the cause of the difference.
- Plain checksums help verify integrity against a trusted reference. They do not independently authenticate the sender of a message.

## Conclusion

The goal of this lab was to practice generating and comparing MD5, SHA-1, and SHA-256 checksums using Windows and Kali Linux tools, and to understand how matching and non-matching hash values can support file integrity verification.
