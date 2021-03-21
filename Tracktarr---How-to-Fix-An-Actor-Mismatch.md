## How to Fix An Actor Mismatch

Say you want to search for all movies by a certain actor/actress, but when you do:

`traktarr movies -t person -a 'christopher lee' -l 100`

It returns movies for an actor called Christopher Ming-Shun Lee instead.

As this is Traktarr, it uses Trakt as the API, so go to http://trakt.tv and search using the dropdown 'People' for Christopher Lee. It will show all results matching him. Click on the correct one and look at the URL:

`https://trakt.tv/people/christopher-lee-720aecc5-2da9-494e-8f93-12811e3e9487`

Now, copy the part after people/ and paste it into where the actors name should be:

`traktarr movies -t person -a 'christopher-lee-720aecc5-2da9-494e-8f93-12811e3e9487' -l 100`

It will now pull down the correct actors movie and load them into Radarr.

_Note: For Mediabox/Feederbox setups, this can be install in either system._ 