getsong is an utility for downloading music videos from YouTube. It comes with
findsong - another utility used to find music videos on YouTube by their name.

## Usage: getsong
getsong is terminal application. You can supply most parameters from terminal
this

```
getsong url artist album name
```

However, this way you won't be able to set the offset and duration of actual
song in the video. To do that, you have to use the interactive mode by
launching getsong without some of its parameters. Usualy, you will want to
launch getsong with just the URL or with no parameters at all:

```
getsong url
--- or ---
getsong
```

In interactive mode, getsong will ask you required information and provide 
default values (URL will be taken from X clipboard, other parameters will be
parsed from the page). To use default values, do not enter anything and just
press Enter.

Songs will be saved in `$HOME/Music/Artist/Album/Name.mp3`

## Usage: findsong
findsong is a wrapper around getsong. It allows you to search for videos from
within the terminal - upon launch, you will be prompted to enter song title
and artist. findsong will then search for YouTube videos using the YouTube
Data API v3 (you have to provide your own API key for this, see Instalation).

Next, you will be given a list of up to five videos, with their extracted music
metadata. Enter the number of video you want to see (and maybe download) and
press Enter (if you don't enter anything, first video will be selected).

The video will be opened in your default browser and getsong will be launched
with its URL. You can check the video is what you were looking for (and when
the song starts and ends) in the browser and then continue the download process
in terminal (you will be in getsong's interactive mode). To cancel the
download, simply press Ctrl+C in the terminal.

## Installation
There are two configuration directories for getsong and findsong: `$CFG` and
`$REG`. `$CFG` holds user configuration such as useragent and YouTube Data API
key, `$REG` holds regular expressions used to extract song metadata from
the page (I know, I know, I shouldn't use regexes to parse HTML, but what
you gonna do, huh? (btw Pull Request with better method of doing this would be
really appreciated ;) ))

By default, both `$CFG` and `$REG` point to `$HOME/.config/getsong`, so that's
where you should copy the contents of `config` directory from this repo if you
don't want to make any changes in the scripts.

If you want to use findsong, you will also have to save your YouTube Data API
v3 key to `$CFG/yt-data-v3.key`. Do not include trailing newline. Safe way:

```
echo "<your key>" > "$CFG/yt-data-v3.key"
```

You probably also want to put your scripts somewhere in your PATH.

## Dependencies
getsong requires xclip (to get default URL from clipboard), ffmpeg, python3
and youtube-dl. youtube-dl needs to be in `$HOME/git/youtube-dl` - if you
wish to change this, open getsong in your preffered text editor, find line

```
cd $HOME/git/youtube-dl
```

And change the path to your youtube-dl installation directory.

findsong requires all of getsong deps (except xclip - getsong will never be
called without URL, so it will never attempt to load clipboard contents) plus
curl and jq - a simple terminal JSON parser.

