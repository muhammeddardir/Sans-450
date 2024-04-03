**Two very common questions :** 
1. "If I have really good endpoint logs, do I need network data?" 
2. "I have really good network data, but don't have good endpoint visibility, is that ok?"

**Answer :**
- First, the short answer is it's always going to be better to have more unique ways to catch malicious activity

Scenario 1 – Malware File
1. A suspicious acting machine with
	1. Traffic to a new IP address associated with an unknown domain
	2. Downloads "calc.exe"
	3. The system is acting funny after the request
	4. We need FAST answers, where do we get them?
2. Scenario 2 –The Failed EDR
	1. You install a new endpoint protection suite (EDR)
	2. Attackers phish and employee using a method the EDR doesn't initially catch
	3. Attackers use their access to disable logging and EDR
	4. Attack continues that device unabated
	5. How do we known if someone has turned off security software?
****
**Email Delivery :**
1. An email may go to an initial MTA designated for mail submission. (MSA)
2. Then Send to intermediate MTA until hit a border MTS for source organization, which the last source organization owned device, that touches the email before it is sent to the destination organization. 
3. The source's border MTA will be passing the message off to the destination's border MTA     (MX record in the DNS logs)
4. To verify the source of the message is legitimate and the email is not spoofed, the destination border MTA may look up the SPF record of the source's border MTA.
5. From destination's border, the message progresses through another potential set of internal MTAs at the destination organization until it reaches the message delivery agent, which will pass the message on to the recipient.
6. After the MUA submits the email to the first MTA (In Source organization), all the subsequent interactions, up until the receiving organization’s MDA receives the email, will utilize the SMTP protocol.
***
**Cobalt Strike's BEACON malware : Search**
***
### Request DNS by dig command
- `dig @8.8.8.8 te.eg A`
- `dig @8.8.8.8 te.eg TXT`
- `dig @8.8.8.8 -x 104.248.50.195` : PTR
***
**Email Attacks :**
- By Pass SMTP Auth and send mail direct to the Border of receiver
	- Prevent this attack using Verifying the Source of a Message as 
		- SPF "Mail source from verified source", DKIM "Message content verified via digital signature", DMARC "Prevents attacks based on different From address and displayed address"

***
**Dynamic Host Configuration Protocol (DHCP)**
1. DHCP Discover: A UDP packet from source IP 0.0.0.0 source port 68 is sent to the broadcast address 255.255.255.255 destination port 67.
2. DHCP Offer: An IP address offer is returned from DHCP server to the user asking for an IP.
3. DHCP Request: Since the client may receive multiple offers if multiple DHCP servers are reachable, the client sends back a DHCP request to the DHCP server that offered the IP it will choose to use. This is also sent to the broadcast address so that all servers that originally responded can read the packet and withdraw their untaken offers.
4. DHCP Acknowledgement: This message is sent back to the client once the offer request has been accepted by the receiving DHCP server.
***
 **When Authentication throw network in event id 4624, 4625 add failed "Network information" contain Authentication Package : NTLM or Kerberos**
 