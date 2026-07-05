# nagios download

### Download Link:- 
https://www.nagios.com/products/nagios-xi/downloads/

-------------------------------------------------------------------------------

extract the file and import it directly into VM 

**user name:- root**

**passwd:- nagiosxi**

now copy the ip provided by nagios and paste it in browser 

**Now do following steps**

- start for free
- Home lab
- fill the name email as you want
- choose a theam modern Dark
- select the time zone -> mumbai
- check the box of  **USe Https only **
- set the password
- setup later
- finish installation

click on Nagios login 

**username = nagiosanmin**

**Password = redhat**

**It will open a dashboard**

### Now 

- Click on **configuration Wizard** menue
- in that search **Linux server** and open it
- it will open a **Linux server configuration wizard**
- now click on link **Download the latest version of NCAP**
- in that select DEB Linux -> **install Using nagios Reps- Deb**

### Now on ubuntu do following steps

```
# Create folder to place the GPG key
  apt-get install apt-transport-https
sudo mkdir -m 0755 -p /etc/apt/keyrings/

# Add the GPG key
curl -fsSL https://repo.nagios.com/GPG-KEY-NAGIOS-V3 | sudo gpg --dearmor -o /etc/apt/keyrings/GPG-KEY-NAGIOS-V3.gpg

# Add the repository with the our GPG key
echo "Types: deb
URIs: https://repo.nagios.com/deb/$(lsb_release -cs)
Suites: /
Signed-By: /etc/apt/keyrings/GPG-KEY-NAGIOS-V3.gpg" | sudo tee /etc/apt/sources.list.d/nagios.sources > /dev/null

# Update your repositories
sudo apt-get update
```
```
cd /usr/local/ncpa
ls 
cd etc
ls
```
### Open the file 

```sudo vim ncpa.cfg```

**in this file go to line no 211 and change **

```community_string = sunny```

save and exit

```sudo systemctl restart ncpa```

```ip -br a```

copy the ip of your client

## Now on Dashbord

in host address = client ip 

token = sunny

next 

check box check  

- ping
- total process = as your wish eg 30
- CPU useage = as your wish eg :- 50
- User Count = give in between 1 - 5

  next

  Finish with defaults

  the you see two links you have to open it
  
  take the screen shorts of it (IT is a monitoring tool in which you can monitor everythign)
