## Initial Analysis

1. `strings` - to get an idea of what the file may have
2. `binwalk` - to check if any other files are embedded in it 
3. `exiftool` - for metadata of the file
4. `hexdump` - check hex of the file (can also use Bless)

[CyberChef](https://gchq.github.io/CyberChef/) and [dCode](https://www.dcode.fr/en) for decoding. 

**Common File formats**

- Archive files (ZIP, TGZ)
- Image file formats (JPG, GIF, BMP, PNG, SVG)
- Filesystem images (especially EXT4)
- Packet captures (PCAP, PCAPNG)
- Memory dumps
- PDF
- Video (especially MP4) or Audio (especially WAV, MP3)
- Microsoft's Office formats (RTF, OLE, OOXML)

## Image Analysis

1. `pngcheck` - to check corruptness and to attempt to repair corrupted PNGs.
2. Steganography - concealing secret data in an image or video. `steghide` for extracting info out of it if you know the passphrase.
3. Gimp - to change aspects of an image like saturation, hue and luminance values.
4. Imagemagick - to resize, crop etc. Also can be used to find differences between two seemingly identical images with `compare`.

## Packet Capture (PCAP) file analysis

PCAP files are used to capture network traffic data. It has raw network packet information, including headers and payloads.

**Filtering**

For initial steps, view the packets in Wireshark. The challenge here usually is that the relevant packets are often drowning in an ocean of unrelated traffic, so you gotta know how to filter the data accordingly.
- Wireshark - tool for analyzing PCAP files. Command line version is `tshark`.
- [DynamiteLab](https://lab.dynamite.ai/) - for getting a graphic display of some timelines of connections and SSL metadata of a PCAP file. It also highlights file transfers and shows you any "suspicious" activity.

**File carving**
- [Xplico framework](https://www.xplico.org/) - for extracting files from a packet capture.

**Repairing a damaged PCAP**
- [PCAPfix](https://f00l.de/hacking/pcapfix.php

## Memory dump analysis

- [Volatility](https://volatilityfoundation.org/) - for analyzing memory dumps

## Video and Audio file analysis

1. `exiftool` - for looking at metadata
2. [Sonic Visualizer](https://www.sonicvisualiser.org/) - for extracting encoded text from an audio waveform.
3. [Audacity](https://www.audacityteam.org/) - for audio file manipulation (slowing down, reverse, etc.)
4. `ffmpeg` - for analyzing and manipulating video files. `ffmpeg -i` gives initial analysis of the file content.
Sometimes, a message may be encoded as [DTMF tones](http://dialabc.com/sound/detect/index.html) or morse code too.