# From various sources, just compiled together here

# Backup git repository
1. `git clone --mirror`
2. `git bundle --all`
source: [StackOverflow](https://stackoverflow.com/q/54468658)

# seperate zips for each directory
source: [SuperUser](https://superuser.com/q/311937)
`FOR %i IN (*.*) DO 7z.exe a "%~ni.7z" "%i"`

# Recording YT Livestream

`streamlink --hls-live-edge 99999 --hls-segment-threads 5 -o "[FILE NAME].ts" [URL] best`
source: [GitHub](https://github.com/rg3/youtube-dl/issues/11618)