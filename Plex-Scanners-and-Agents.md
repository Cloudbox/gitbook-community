# Absolute Series Scanner and HAMA role for anime.

Install the [Absolute Series Scanner (A.S.S.)](https://github.com/ZeroQI/Absolute-Series-Scanner) and the [HTTP Anidb Metadata Agent (HAMA)](https://github.com/ZeroQI/Hama.bundle)

`cd ~/community`

`sudo ansible-playbook community.yml --tags asshama`

# Extended Personal Media Scanner and Agent role
Installs the [Extended Personal Media Shows scanner and agent (EPMS)](https://bitbucket.org/mjarends/extendedpersonalmedia-agent.bundle/src/master/README.md) Useful for sports or things that do not have a DB to scrape against, creates episode numbers for date-based media and sorts correctly in Plex interface.

`cd ~/community`

`sudo ansible-playbook community.yml --tags epms`