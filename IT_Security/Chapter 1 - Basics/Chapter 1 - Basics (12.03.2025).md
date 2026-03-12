>[!SUMMARY]- Table of Contents
>- [[Chapter 1 - Basics (12.03.2025)#Motivation for Attackers|Motivation for Attackers]]
>   - [[Chapter 1 - Basics (12.03.2025)#Classic attackers|Classic attackers]]
>   - [[Chapter 1 - Basics (12.03.2025)#Development in the last decade|Development in the last decade]]
>   - [[Chapter 1 - Basics (12.03.2025)#Shadow economy in cybercrime|Shadow economy in cybercrime]]
>- [[Chapter 1 - Basics (12.03.2025)#Attack types - Overview/Example|Attack types - Overview/Example]]
>   - [[Chapter 1 - Basics (12.03.2025)#Untargeted attacks|Untargeted attacks]]
>   - [[Chapter 1 - Basics (12.03.2025)#Targeted attacks|Targeted attacks]]
>   - [[Chapter 1 - Basics (12.03.2025)#Advanced persistent threads (APT)|Advanced persistent threads (APT)]]
>   - [[Chapter 1 - Basics (12.03.2025)#Example: Log4Shell|Example: Log4Shell]]
>   - [[Chapter 1 - Basics (12.03.2025)#Example: Critical infrastructure|Example: Critical infrastructure]]
>   - [[Chapter 1 - Basics (12.03.2025)#Example: Facebook|Example: Facebook]]
>   - [[Chapter 1 - Basics (12.03.2025)#Example CMC Group Ransomware Attack (12 April 2025)|Example CMC Group Ransomware Attack (12 April 2025)]]
>- [[Chapter 1 - Basics (12.03.2025)#The Communication Model of IT Security|The Communication Model of IT Security]]
>- [[Chapter 1 - Basics (12.03.2025)#Security Objectives and Attack Scenarios|Security Objectives and Attack Scenarios]]
>   - [[Chapter 1 - Basics (12.03.2025)#Security Objectives (aka Protection Goals)|Security Objectives (aka Protection Goals)]]
# Motivation for Attackers
## Classic attackers
- **White hat**: uncovering security gaps 
	- `pentester` or penetration tester (red team)
	- vulnerability (backdoor, bugs,...) 
		- buffer overflow (Bosch: fuggy????)
- **Secret services**: espionage (spying), sabotage (create damage) and surveillance
	- National security
- **Companies:** industrial espionage (cooperation with secret services)
## Development in the last decade
- **Establishment of a highly professionalized shadow economy in cybercrime** (black hat, contract hacking)
- **Publication of secret information** (whistleblower) wanting to public the wrongdoings/ unethical work???
- **Politically** motivated attacks (want to do something regarding about national scope, a higher level)
## Shadow economy in cybercrime
- A lot of money can be made with successful attacks
	- **Bitcoin mining:** 
		- hash value? nonce or number used once = number (example 2 bits) 
			- nonce + prob block's hash = new hash in specific format (ex: 2 last digits are '0')
		- To mind the nonce, or minding the coin without the owner permission
	-  **Phishing attacks in the area of online banking:** the attack impersonate and send a malicious link -> comp becomes compromise.  
	- Accessing credit card information (commercial credit card fraud): apply AI to check if the transaction classify/predict if fraud

In addition, there is an established black market for software vulnerabilities of IT systems (other word = exploits)

# Attack types - Overview/Example
## Untargeted attacks
Mass emails for distributing viruses (to be activated, someone has to trigger it with an external action), worm (standalone, self-replicating programs that spread automatically across networks without human intervention) and Trojans (stand still until one day execute) or launching phishing attacks.
## Targeted attacks
Sabotage and espionage aimed at certain institutions (DDoS attacks on state infrastructures) -> Create pressure (Tân Sơn Nhất attack)

## Advanced persistent threads (APT)
Targeted sabotage on certain IT system (Stuxnet). 
Example: 
- Certificate service provider (forgery of SSL certificates from the Dutch company   `DigiNotar` in July 2011, this also affected the server certificate from google.com).
- Attack on computer system of the Democratic Party in the run-up to the US   presidential election in 2016
## Example: Log4Shell
**November/December 2021**: A vulnerability has been discovered in the widely used logging software Log4j for Java "Worst vulnerability ever."
## Example: Critical infrastructure
**May 2021 Colonial pipeline**: Colonial, which operates a pipeline transporting petrol from Texas to New Jersey and the Midwestern United States, was disrupted by ransomware malware....

ransomware: encrypts a victim’s data or locks their system, demanding cryptocurrency payment to restore access. These attacks often involve "double extortion," where data is also stolen and threatened with release. Major types include screen-lockers, file-encryptors, and wiper malware.

Backdoor: The VGU use old window server because of that in 2017 they got attacked 3 times. Yet because website is isolated, not much damaged have been done. 

sth sth Dương Ngọc Thái 
## Example: Facebook
**April 2021**: Data leak at Facebook, cybercriminals stole data from 533 million Facebook users from Facebook servers. This was due to a misconfiguration in the function used by Facebook to import data from users' smartphones.  

## Example CMC Group Ransomware Attack (12 April 2025)
Attack on CMC Corporation, Vietnam, by Crypto24 ransomware group. Attackers infiltrated CMC's private cloud environment, creating unauthorized administrator accounts.  2 TB of sensitive data, including tokens,  databases, and website assets, were compromised. Core services remained operational, the  data breach triggered police investigation.
# The Communication Model of IT Security
**Actors:** Alice, Bob and Mallory
- Alice and Bob exchange messages over an insecure communication channel
- Mallory tries everything to attack the communication between Alice and Bob. A Man-in-the-Middle (MitM).

![[Pasted image 20260312113744.png|509]]

**Mallory's skills and capabilities:** 
- **Passive attack**: eavesdrop on the line. (only reading/listening but do nothing)
- **Active attack**: (the danger is on point)
	- **Digital**: manipulate the line
	- **Physical**: cut the line (physical infrastructure)
# Security Objectives and Attack Scenarios
## Security Objectives (aka Protection Goals)
