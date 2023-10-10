
![[DALL·E 2023-08-07 20.08.52 - visualize audio space from the heavans.png]]
*DALL-E: visualize audio space from the heavans*

# Issue

I'm a slacker and don't read traditional books. I ingest plenty of articles online day to day though.

I want to listen to [Mountaineering: Freedom of the Hills](https://www.amazon.com/gp/product/B076H9532R/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)

# Goal

I want to play this book audibly on my phone while driving. To pull that off my plan was:
1. Get the eBook (Amazon Kindle)
2. Convert to text ([calibre](https://calibre-ebook.com/))
3. Create mp3 to listen to on my phone ([Spotify](https://support.spotify.com/us/article/local-files/) and maybe OneDrive to get it over there or something)

# Converting to Text

I'm unable to get past the DRM.

So I downloaded the epub from https://libgen.rocks/index.php
> ![Fail]
> I do not condone illegal activity. You should pay for ebooks.

I did [install Clam AV](https://askubuntu.com/questions/417429/how-can-i-scan-for-possible-viruses-on-my-ubuntu-system) and scanned the file...

Install Calibre
```
sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin
```

Convert epub to txt
```
ebook-convert source.epub out.txt
```

> [!Info] This created a `1.9 MB` text file with `1,924,541` characters


I manually edited some of the beginning and index. No automated way to do that to with raw text to my knowledge. This brought the file to `1.8 MB` and `1,811,393` characters.

# Creating Audio

I spent a little bit of time looking into:
- https://github.com/mozilla/TTS
- https://aws.amazon.com/polly/

For the sake of time I decided to go the paid route with Amazon Polly.

Unfortunately, Polly only accepts 100K [characters at a time](https://docs.aws.amazon.com/polly/latest/dg/limits.html). So we need to split up the file:
```
split -b100000 out.txt
```

> [!Info] You need the aws cli installed and a bucket for the next steps, swap out the bucket `lkat`

Upload the text file to S3:

```
aws s3 cp ./out.txt s3://lkat/audiobooks/freedom-of-the-hills/out.txt
```

> [!Error] This **will** cost money

```
aws polly start-speech-synthesis-task \ --engine `standard` --region `us-east-1` \ --endpoint-url "`https://polly.us-east-1.amazonaws.com/`" \ --output-format mp3 \ --output-s3-bucket-name `lkat` \ --output-s3-key-prefix `audiobooks/freedom-of-the-hills` \ --voice-id Joey \ --text `file://out.txt`
```

# File Management
I decided to merge all files 

# Mobile Play

### Original Plan
Now that the mp3's are generated, lets make them available on your phone via Spotify.

I originally thought that I needed Onedrive to sync files, enable local files on mobile, and then point to the files on Onedrive. *This is **not** the way*.

### Better Way
[This article](https://sports.yahoo.com/upload-local-music-spotify-play-184024446.html)

**On Spotify desktop**:
* Enable *Show Local Files*
- Add the folder with you mp3s with *Add a source*
- Create a playlist
- Go to your Library and then *Local Files*, multi-select your mp3s, right click, add to your playlist

**On Spotify mobile**:
- Click your playlist
- Choose download playlist

Now you have your audio book with Spotify tracking your listen history 🎉



Already did:
- https://us-east-1.console.aws.amazon.com/polly/home/SynthesisTasks/b345cffd-dd54-4119-8d04-6daa1866d806
- https://us-east-1.console.aws.amazon.com/polly/home/SynthesisTasks/b6427607-4ca4-4530-acbb-0da61934349b



# Thought Stream
* [bash - How to split text files by character count in directory - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/595790/how-to-split-text-files-by-character-count-in-directory)
* [Neural TTS - Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/NTTS-main.html)
* [Quotas in Amazon Polly - Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/limits.html)
* [iterate through files bash - Google Search](https://www.google.com/search?q=iterate+through+files+bash&oq=iterate+through+files+bash&aqs=chrome..69i57j0i22i30l9.5152j0j7&sourceid=chrome&ie=UTF-8)
* [windows - Downloading folders from aws s3, cp or sync? - Stack Overflow](https://stackoverflow.com/questions/27932345/downloading-folders-from-aws-s3-cp-or-sync)
* [How to merge MP3 files Linux - Linux Tutorials - Learn Linux Configuration](https://linuxconfig.org/joining-mp3-music-files-to-a-single-track)
* [Concatenate – FFmpeg](https://trac.ffmpeg.org/wiki/Concatenate)
* [bash - How to rename with prefix/suffix? - Stack Overflow](https://stackoverflow.com/questions/208181/how-to-rename-with-prefix-suffix)
* [Local files - Spotify](https://support.spotify.com/us/article/local-files/)
* [How to upload local music to Spotify so you can play songs stored on your computer, even when offline](https://sports.yahoo.com/upload-local-music-spotify-play-184024446.html)
* [format conversion - How can I convert .epub files to plain text? - Ask Ubuntu](https://askubuntu.com/questions/102458/how-can-i-convert-epub-files-to-plain-text)
* * [How to Transfer Any eBook to Kindle Using Calibre](https://www.howtogeek.com/539829/how-to-transfer-any-ebook-to-kindle-using-calibre/)
* [Download Books to Your Kindle App - Amazon Customer Service](https://www.amazon.com/gp/help/customer/display.html?nodeId=GD2V96KJZJ6PL3FL)
* [How to transfer library Kindle Books via USB](https://help.overdrive.com/en-us/0448.html)
* [Digital Rights Management (DRM) — calibre 6.24.0 documentation](https://manual.calibre-ebook.com/drm.html)
* [apprenticeharper/DeDRM\_tools at v7.2.1](https://github.com/apprenticeharper/DeDRM_tools/tree/v7.2.1)
* [DeDRM\_tools/FAQs.md at master · apprenticeharper/DeDRM\_tools](https://github.com/apprenticeharper/DeDRM_tools/blob/master/FAQs.md)
* [rupor-github/fb2converter: Unified converter of FB2 files into epub2, kepub, mobi and azw3 formats.](https://github.com/rupor-github/fb2converter)
* [How to Remove DRM From AZW3 Kindle](https://epubor.com/remove-drm-from-azw3.html)
* [instructions for converting all of your DRM’d Kindle books into a non-DRM format that you can read on any number of devices. | Slade Knowledge Base](https://www.ucl.ac.uk/slade/know/2979)
* [kevinxiong/epub2txt: convert epub file to txt](https://github.com/kevinxiong/epub2txt)
* [golang epub parser - Google Search](https://www.google.com/search?q=golang+epub+parser&oq=golang+epub+parser&aqs=chrome..69i57j0i22i30.4460j0j7&sourceid=chrome&ie=UTF-8)
* [kevinboone/epub2txt2: A simple command-line utility for Linux, for extracting text from EPUB documents.](https://github.com/kevinboone/epub2txt2)