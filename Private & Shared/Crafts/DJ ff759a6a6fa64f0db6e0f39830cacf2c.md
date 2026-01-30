# DJ

## Controller

Serato DJ

Hercules DJControl Starlight

[https://www.amazon.ca/Hercules-DJCONTROL-STARLIGHT-DJControl-Starlight/dp/B07F8FQ8ST?th=1](https://www.amazon.ca/Hercules-DJCONTROL-STARLIGHT-DJControl-Starlight/dp/B07F8FQ8ST?th=1)

---

# Music Pipeline

## Philosophy

1. Local folders on disc are **Cold Storage,** sorted by **Genre**. Even if:
- a Trance track lives in House
- or a Techno track lives in Trance

It doesn’t matter — because **you won’t DJ from folders**.

1. Serato Crates are **vibe + function**, not genre. Examples of **good crates**:
- Warm-Up
- Groovy / Funky
- Peak-Time

Notice: none of these say “House” or “Trance”.

1. Tag files using comments metadata of files
- groovy | funky | warmup | long intro | energy:3

Let Serato *interpret* your tags — don’t let it *own* them.

## Downloading

### Nicotine

Nicotine+ is a UI wrapper for SoulSeek - Peer share for songs

https://nicotine-plus.org/doc/DOWNLOADS.html#macos

### Soundcloud

[https://sclouddownloader.net/](https://sclouddownloader.net/)

- Playlist Export
    
    ### Spotify Playlist
    
    Exportify - export Spotify to csv
    
    [https://watsonbox.github.io/exportify/](https://watsonbox.github.io/exportify/)
    
    ### Import via Soundizz
    [https://soundiiz.com/webapp/playlists](https://soundiiz.com/webapp/playlists)
    
    ### Spotify to Tidal
    
    [https://www.tunemymusic.com/home?id=spotify-to-tidal](https://www.tunemymusic.com/home?id=spotify-to-tidal)
    
- Other
    
    ### Spotify
    
    Do not attempt, you will be caught
    
    [Python for Spotify - Sync Playlist](DJ/Python%20for%20Spotify%20-%20Sync%20Playlist%202f73e425b6824a08b14bf79bf35a98ca.md)
    

---

## Local File Management

### Step 1: Mp3Tag

https://www.mp3tag.de/en/

- Setup
    
    Setup Action Group
    
    - Go to **Actions → Actions…**
    - Click **New**
    - Name it: **DJ – Normalize Tags (v1)**
        - Add action:
        - Click **New**
        - Choose **Replace with regular expression**
        - Field: `GENRE`
        - Replace:
            
            ```
            (?i).*house.* 
            ```
            
        - With:
        
        ```
        House
        ```
        

1. First use Mp3Tag to set Genre for all downloaded files
    1. Run **DJ – Normalize Tags (v1)**
    2. Manually fix any blank or wrong genres
2. Additionally, you can use search features to try to fill out metadata if you chose

### Step 2: MusicBrainz Picard

https://picard.musicbrainz.org/

- Setup
    
    Make sure Options →  Move Files is checked
    
    ```jsx
    Library/$if2(%genre%,'Uncategorized')/ %artist% - %title%
    ```
    

1. Select Niccotine folder
2. highlight all songs and click ‘Scan’
3. With songs that don’t cluster … Save manually?

→ Saving clustered files will THEN move files to location

### Step 3: Mp3Tag

- Setup
    
    ```jsx
    %artist% - %title%
    ```
    

1. Finally, back in Mp3Tag,  open the entire genre folder you want e.g. ‘House’
2. Sort by empty comments
3. rename files based on tags, to %title% - %artist%
4. Fill in comments manually for detailed info on songs

## Serato Crates

---

## Serato Crate Organization

## Categorization

Use some tools to help categorize?

[https://www.discogs.com](https://www.discogs.com/release/14981755-Fasme-Stretched-World)

[https://www.last.fm](https://www.last.fm/music/FASME/Stretched+World)

Very Specific

[https://everynoise.com/](https://everynoise.com/)

Takes in entire playlist library!

[http://organizeyourmusic.playlistmachinery.com/#](http://organizeyourmusic.playlistmachinery.com/#)

Potentially this to mass categorize music files and write metadata directly to files

[https://onetagger.github.io/#about](https://onetagger.github.io/#about)