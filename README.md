# bloodhound-quickwin
Simple script to extract useful information and potential quick wins from BloodHound and Neo4j.

## Prerequisites
- python3
```bash
sudo pip3 install py2neo
sudo pip3 install pandas
```
## Example
- Use your favorite [collectors](https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors) to gather "./zip or .json"
- Start your neo4j console
- Import "./zip or .json" in [bloodhound](https://github.com/BloodHoundAD/BloodHound)
- Run ./bhqc.py

## Usage
```bash
kaluche@pwn $ ./bhqc.py -h
usage: bhqc.py [-h] [-b BOLT] [-u USERNAME] [-p PASSWORD]

Lists out some good quick wins from BloodHound and Neo4j. SharpHound collections must be loaded into BloodHound before running this.

Optional arguments:
  -h, --help            Show this help message and exit
  -b BOLT, --bolt BOLT  Neo4j bolt connection (default: bolt://127.0.0.1:7687)
  -u USERNAME, --username USERNAME
                        Neo4j username (default : neo4j)
  -p PASSWORD, --password PASSWORD
                        Neo4j password (default : neo4j)
```


## Output
```bash
SV1@kali $ ./bhqw.py

##################################################################################
[*] Enumerating all domain admins - Groups and Users (rid:512|544) (recursive)
##################################################################################

[+] Domain admins (group) 	  : DOMAIN ADMINS@FBC.LAB
[+] Domain admins (group) 	  : ENTERPRISE ADMINS@FBC.LAB
[+] Domain admins (group) 	  : FBCDIRECTION@FBC.LAB
[+] Domain admins (enabled) 	: ADMINISTRATOR@FBC.LAB [LASTLOG: < 1 year]
[+] Domain admins (enabled) 	: DIRECTOR.TRENCH@FBC.LAB [SPN] [LASTLOG:  NEVER]
[+] Domain admins (enabled) 	: CASPER.DARLING@FBC.LAB [ASREP] [LASTLOG:  NEVER]

##################################################################################
[*] Enumerating enabled SPN service/user accounts (KERBEROASTING)
##################################################################################

[+] SPN DA (enabled) 	: DIRECTOR.TRENCH@FBC.LAB

##################################################################################
[*] Enumerating enabled AS-REP service/user accounts  (AS-REP ROASTING)
##################################################################################

[+] AS-REP Roastable DA (enabled) 	: CASPER.DARLING@FBC.LAB

##################################################################################
[*] Enumerating all service/user accounts with SPN set
##################################################################################

[+] SPN (enabled) 	: DYLAN.FADEN@FBC.LAB
[+] SPN (enabled) 	: ATHI@FBC.LAB
[+] SPN (enabled) 	: EMILY.POPE@FBC.LAB
[+] SPN (enabled) 	: DIRECTOR.TRENCH@FBC.LAB [AdminCount]
[+] SPN (enabled) 	: JESSE.FADEN@FBC.LAB
[+] SPN (disabled) 	: KRBTGT@FBC.LAB [AdminCount]

##################################################################################
[*] Enumerating all service/user accounts that are AS-REP Roastable
##################################################################################

[+] AS-Rep Roastable (enabled) 	: FREDERICK.LANGSTON@FBC.LAB
[+] AS-Rep Roastable (enabled) 	: CASPER.DARLING@FBC.LAB [AdminCount]

##################################################################################
[*] Enumerating Unconstrained Delegation Accounts
##################################################################################

[+] Unconstrained Delegation (enabled) 	: JESSE.FADEN@FBC.LAB

##################################################################################
[*] Enumerating Constrained Delegation User Accounts
##################################################################################

[+] Constrained Delegation (enabled) 	: DYLAN.FADEN@FBC.LAB ['snmp/dc1.FBC.LAB']

##################################################################################
[*] Enumerating Unconstrained Computer Accounts
##################################################################################

[+] Unconstrained computers (enabled) : DC1.FBC.LAB [Windows Server 2016 Standard]

##################################################################################
[*] Statistics
##################################################################################

+--------------------------------------------+------------+-------+
|                Description                 | Percentage | Total |
+--------------------------------------------+------------+-------+
|                 Total users                |    N/A     |   21  |
|             Total enabled user             |   85.71    |   18  |
|            Total disabled users            |   14.29    |   3   |
|     Users with 'Domain Admin' rights       |   16.67    |   3   |
|      All users not logged in > 6 months    |    0.0     |   0   |
|    Enabled users not logged in > 6 months  |    0.0     |   0   |
| Password not changed > 1y  (enabled)       |    0.0     |   0   |
| Password not changed > 2y  (enabled)       |    0.0     |   0   |
| Password not changed > 5y  (enabled)       |    0.0     |   0   |
| Password not changed > 10y (enabled)       |    0.0     |   0   |
|      Kerberoastable users with SPN         |   33.33    |   6   |
|      AS-REP Roastable users                |   11.11    |   2   |
|  Enabled users that has never logged in    |   88.89    |   16  |
+--------------------------------------------+------------+-------+

```
