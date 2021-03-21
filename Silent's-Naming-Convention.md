My naming convention....

## sonarr:

**Series Folder Format:** `{Series TitleYear}`

**Standard Episode Format:** `{Series CleanTitle} - S{season:00}E{episode:00} [{Quality Title} {MEDIAINFO VIDEO} {MediaInfo AudioCodec} {MediaInfo AudioChannels}]{-Release Group}`

**Daily Episode Format:** `{Series CleanTitle} - {Air-Date} [{Quality Title} {MEDIAINFO VIDEO} {MediaInfo AudioCodec} {MediaInfo AudioChannels}]{-Release Group}`

**Anime Episode Format:** 
`{Series CleanTitle} - S{season:00}E{episode:00} [{Quality Title} {MEDIAINFO VIDEO} {MediaInfo AudioCodec} {MediaInfo AudioChannels}]{-Release Group}`

**Example:**

`Single Episode: The Series Title! - S01E01 [HDTV-720p X264 DTS 5.1]-RlsGrp.mkv`

`Multi Episode: The Series Title! - S01E01-E03 [HDTV-720p X264 DTS 5.1]-RlsGrp.mkv`
## sonarr4k:

Same as above.

## radarr:
**Standard Movie Format:** `{Movie Title} ({Release Year}) {Edition Tags} [{Quality Title} {MEDIAINFO VIDEO} {MediaInfo AudioCodec} {MediaInfo AudioChannels}]{-Release Group}`

**Example:** `The Movie Title (2010) Ultimate Extended Edition [Bluray-1080p X264 DTS 5.1]-EVOLVE.mkv`

## radarr4k (**requires** nightly Radarr branch for HDR tag):
**Standard Movie Format:** 
`{Movie Title} ({Release Year}) {Edition Tags} [{Quality Title} {MEDIAINFO HDR} {MEDIAINFO VIDEO} {MediaInfo AudioCodec} {MediaInfo AudioChannels}]{-Release Group}`

**Example:** `The Movie Title (2010) Ultimate Extended Edition [Remux-2160p HDR HEVC DTS-HD MA 5.1]-EVOLVE.mkv`



