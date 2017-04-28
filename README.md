#Send To DNS

Sharing files using DNS

##What is this?

This project is designed to allow users to share files using the Domain Name System (DNS). The Domain Name System supports DNS cache servers which store DNS query results for a period of time determined in the configuration (time-to-live) of the domain name record in question. This feature allows files stored on an authoritative name server to be cached on nameservers closer to the end-user, and allows for easy replication of the file across any recursive nameservers.

As a proof of concept, the code is written to use the bind nsupdate tool to perform dynamic updates to a bind server. Easier methods can be devised both for bind, and other nameservers such as writing the records directly to a zone file, or taking advantage of the varied backend technologies that servers such as PowerDNS provide.

A file can be requested just by using it's generated identifier, all meta-information about records used, length and md5 is stored with the file in DNS.

    # dig TXT  short  vc fileid.4qefx5.sendtodns.org 
    "ubuntu-11.10-desktop-i386.iso,4qefx5.001,4qefx5.696,c396dd0f97bd122691bdb92d7e68fde5"
    #
    # dig TXT  short  vc fileid.4qefx5.001.sendtodns.org
    "4qefx5.001,459,cdbbc5f3ab446f078ce57f1c2a29c781"
    #

In the proof of concept, files are broken apart using 'lxsplit' and then converted to text using uuencode. The split files are then pushed to TXT records with a random name.

---

##Try it out!

This example runs a shell script that will pull down a 45M version of the movie Elephants Dream. You can read the script [here](https://raw.github.com/gist/2f5d143612734f321fa2) before running.

    bash -s < <(curl -fsSL https://raw.github.com/gist/2f5d143612734f321fa2) e8fkiy

---

##[Download Latest version from GitHub](https://github.com/sendtodns/sendtodns/zipball/master)

---

###Disclaimer
The code is functional but ugly. Part of the reason for creating this is to get more familiar with Ruby. PLEASE fork the code and submit pull requests, even if you are just adding a TODO.txt with a list of things I should clean up.
