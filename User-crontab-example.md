Example user crontab for cloudbox users.

Note that this is just one example, not a list of things that any particular user should have in their crontab.

`crontab -e`

```
@daily bash /opt/python-plexlibrary/plexlibrary.sh
0 7 * * 7 sudo PATH='/usr/bin:/bin:/usr/local/bin' env ANSIBLE_CONFIG='/home/seed/cloudbox/ansible.cfg' '/usr/local/bin/ansible-playbook' '/home/seed/cloudbox/backup.yml' -v  >> '/home/seed/logs/cloudbox_backup.log' 2>&1
@daily curl -s https://cloudbox.works/scripts/repo.sh | bash >/dev/null && cd ~/cloudbox
* * * * * /opt/scripts/nzbget/cleanup.sh
0 10 * * * /opt/scripts/plex/optimize.sh
0 * * * * PATH='/usr/bin:/bin:/usr/local/bin' cd /opt/SonarrSync/ ; /usr/bin/python SonarrSync.py
```

**Line 1:** `python-plexlibrary` script to make Plex libraries. - [Runs midnight daily **server time**]

**Line 2:** Cloudbox backup. - [Runs every Sunday @ 7AM **server time**]

**Line 3:** [Cloudbox repo.sh script to update Cloudbox and do auto-updates for you](https://github.com/Cloudbox/Cloudbox/wiki/Install%3A-Dependencies) - [Runs daily]

**Line 4:** cleanup script to remove left over junk in /downloads/nzbs/nzbget/completed/sonarr/* etc. - [Runs every minute] `Note: Scroll down for a couple ideas for this script.`

**Line 5:** Script to optimize the Plex database. - [Runs daily @ 10AM **server time**] 
`Note: Scroll down for script.`

**Line 6:** [Enormoz's SonarrSync](https://github.com/EnorMOZ/SonarrSync) (based on Sperryfreak's RadarrSync) - [Runs hourly]

***
### pho's cleanup.sh
This script deletes 
* everything under a size of 100M
* every unwanted file immediately
* everything but the wanted files after 10 hours
* every empty folder

```bash
#!/bin/bash
#####################################################
# script by pho
#####################################################

# basic settings
TARGET_FOLDER="/mnt/local/downloads/nzbs/{sabnzbd,nzbget}/completed/{radarr,sonarr,lidarr}/" # find files in this folders
FIND_SAMPLE_SIZE='100M' # files smaller then this are seen as samples and get deleted

# advanced settings
FIND=$(which find)
FIND_BASE_CONDITION_WANTED='-type f -amin +600'
FIND_BASE_CONDITION_UNWANTED='-type f'
FIND_ADD_NAME='-o -iname'
FIND_DEL_NAME='! -iname'
FIND_ACTION='-not -path "*_UNPACK_*" -delete > /dev/null 2>&1'
command="${FIND} ${TARGET_FOLDER} -mindepth 1 ${FIND_BASE_CONDITION_WANTED} -size -${FIND_SAMPLE_SIZE} ${FIND_ACTION}"
#echo "Executing ${command}"
eval "${command}"

WANTED_FILES=(
    '*.mkv'
    '*.mpg'
    '*.mpeg'
    '*.avi'
    '*.mp4'
    '*.mp3'
    '*.flac'
    '*.srt'
    '*.idx'
    '*.sub'
)
UNWANTED_FILES=(
    '*.nfo'
    '*.jpeg'
    '*.jpg'
    '*.gif'
    '*.rar'
    '*sample.*'
    '*.sh'
    '*.pdf'
    '*.doc'
    '*.docx'
    '*.xls'
    '*.xlsx'
    '*.xml'
    '*.html'
    '*.htm'
    '*.exe'
    '*.nzb'
)
#Folder Setting
condition="-iname '${UNWANTED_FILES[0]}'"
for ((i = 1; i < ${#UNWANTED_FILES[@]}; i++))
do
    condition="${condition} ${FIND_ADD_NAME} '${UNWANTED_FILES[i]}'"
done
command="${FIND} ${TARGET_FOLDER} -mindepth 1 ${FIND_BASE_CONDITION_UNWANTED} \( ${condition} \) ${FIND_ACTION}"
#echo "Executing ${command}"
eval "${command}"

for ((i = 0; i < ${#WANTED_FILES[@]}-1; i++))
do
    condition2="${condition2} ${FIND_DEL_NAME} '${WANTED_FILES[i]}'"
done
command="${FIND} ${TARGET_FOLDER} -mindepth 1 ${FIND_BASE_CONDITION_WANTED} \( ${condition2} \) ${FIND_ACTION}"
#echo "Executing ${command}"
eval "${command}"

command="${FIND} ${TARGET_FOLDER} -mindepth 1 -type d -empty ${FIND_ACTION}"
#echo "Executing ${command}"
eval "${command}"

```
### RXWatcher's cleanup.sh

Note that this script is specific to its author's setup when it was written.  It probably won't work for you as-is.  You'll need to edit the paths to match your situation.

```Bash
#!/bin/bash
find /mnt/local/downloads/nzbget/completed/sonarr/* -type d -mmin +60 -ls -exec rm -rf {} + 2>/dev/null
find /mnt/local/downloads/nzbget/completed/radarr/* -type d -mmin +60 -ls -exec rm -rf {} + 2>/dev/null
find /mnt/local/downloads/nzbget/completed/books/*  -type d -mmin +240 -ls -exec rm -rf {} + 2>/dev/null
find /mnt/local/downloads/nzbget/completed/sonarr/* -type d -mmin +60 -ls -exec rm -rf {} + 2>/dev/null
find /mnt/local/downloads/nzbget/completed/radarr4k/* -type d -mmin +60 -ls -exec rm -rf {} + 2>/dev/null
find /mnt/local/downloads/nzbget/completed/anime/* -type d -mmin +60 -ls -exec rm -rf {} + 2>/dev/null
```

***

### RXWatcher's optimize.sh
```Bash
#!/bin/sh
# Get the contents of the Preferences file, keep only what we need,  push to a temp, then use it in the curl command

cat "/opt/plex/Library/Application Support/Plex Media Server/Preferences.xml" |  \
sed -e 's;^.* PlexOnlineToken=";;' | sed -e 's;".*$;;' | tail -1 > /tmp/plex.tmp

curl --request PUT http://127.0.0.1:32400/library/optimize\?async=1\&X-Plex-Token=`cat /tmp/plex.tmp`

rm -f /tmp/plex.tmp
```