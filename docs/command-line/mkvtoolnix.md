# Mkvtoolnix

Mkvtoolnix is a commandline tool which allows you to modify mkv files and extract from or merge other files with. I use mkvtoolnix to edit the movies that go into my media library. This is a quick overview of commands I use frequently.

## Mkvextract

With mkvextract you can extract certain tracks from mkv files. The most simple usage of this is as follows:

```bash
mkvextract <filename> tracks 0:video 1:audio 2:subtitles
```

In this command, the numbers are the track numbers. You can get these with [mkvmerge](/wiki/command-line/mkvtoolnix/#mkvmerge). 

You can rename the extracted files by adjusting the name after the number. For example: `2:"Hello, world!.txt"` would generate a file that's called `Hello, world!.txt` from the mkv. Do keep an eye on the format of the files, because you can't really have videos with a `.txt` extension.

## Mkvmerge

With mkvmerge, you can merge files within an mkv container. It also has a `--identify` flag, which allows you to get track numbers you might use for [mkvextract](/wiki/command-line/mkvtoolnix/#mkvextract) or mkvmerge itself. This can be done by running a simple command:

```bash
mkvmerge --identify <filename>
```

To merge files with mkvmerge, you can use the `-o` flag to specify and output file and just add your files after.

```bash
mkvmerge -o example-movie.mkv example-video.avi example-audio.ogg
```

You can also specify the language for a certain file, for example the previous command would be adjusted as follows:

```bash
mkvmerge -o example-movie.mkv example-video.avi --language 0:en example-audio.ogg
```

The language just uses a two character language code. You can do a lot more with mkvtoolnix, check out the full documentation on their [site](https://mkvtoolnix.download/docs.html).
