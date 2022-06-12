# Image Upload 

## Misc - 50 pts (257 Solves)

HTTP is not secure. Inspect this packet dump and you will know why.

Find the packet related to an image upload and extract the image. Then, find the name of the creator of this image.

Files: dump.pcap

# Solution

We are given a `.pcap` file, which we can open and view using [Wireshark](https://www.wireshark.org/).

We can search for the uploaded image by:

1. Filtering for `http.request`, or
2. Going to `File > Export Objects > HTTP`

If we view the information in this, we find Textual data in a tEXt, and it has the Author `akashchandrasekaran_grey{wireshark_exiftool_are_good}`. Here is our flag!

# Flag

`grey{wireshark_exiftool_are_good}`