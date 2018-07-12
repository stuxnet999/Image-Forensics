# __Image Forensics__

#### What is Image Forensics?

To keep it very simple and straight, **Image Forensics** is a specific branch of cyber forensics which deals with a various number of attacks.

Some of them include:

1. The authenticity of an image

2. Detection of possible forgeries etc.

So let us look into some of the very basic definitions of the technical terms used in this field to better understand the upcoming topics.

#### **File Signature**:

A typical file signature is something which defines the nature of a file and also tells us about the specific features of the particular file. This is also called as the file header or sometimes as the checksum.

So let us look at some examples:

1. PNG -> **89 50 4E 47 0D 0A 1A 0A**

2. ZIP FILE -> **50 4B 05 06**

The 'hex' values shown are also called as **magic numbers.**

#### **Chunks**:

Chunks are nothing but fragments of information used by different multimedia formats like **PNG, MP3** etc.
Each chunk has its own header. The header usually describes the type and size of the chunk.

![alt text](https://github.com/stuxnet999/Image-Forensics/blob/master/Chunk_example.png "Chunk example")

**How important are chunks ?**

So let us consider that you are trying to open an image using a MP3 player.
Will the player open the image? No, right.
It'll give me an error message. Every application has a decoder which checks the type of the chunks given. When it recognizes that the given chunks are supported, it tries to give the desired output. So whenever it comes across chunks of unknown format, it triggers an error message stating **"Unsupported File Format"**


#### **Cyclic Redundant Checksum**:

Cyclic redundant checksum(CRC) is an integral value which represents the sum of correct digits in a piece of data.
Checksums help us to check the data integrity of a file which is transmitted across the digital network.
There are many checksum algorithms. Checksum algorithms are employed in various cybersecurity concepts like **fingerprinting, cryptographic hash functions** etc. 

&nbsp;

So now let us look at the file format of a **PNG** image:

#### Portable Network Graphics (PNG):

A PNG is a graphical file format of an image which supports **lossless compresion**.

**Magic Number** -> **89 50 4E 47 0D 0A 1A 0A**

![alt text](https://github.com/stuxnet999/Image-Forensics/blob/master/PNG_File-Header.png "PNG File Header")

So now let us look at the critical chunks of a PNG image:

#### **Critical chunks** :

**IHDR** -> Describes image dimensions, color type, bit depth etc. It must be noted that this must be the first chunk (always).

**PLTE** -> Contains the list of colours.

**IDAT** -> Contains the image data.

**IEND** -> Marks the end of the image.

#### **Ancillary chunks** :
Ancillary chunks can be otherwise called as optional chunks. These are the chunks which are generally ignored by decoders.
Let us look at some examples:

**bKGD** -> Gives the default background colour.

**dSIG** -> This chunk is used to store the digital signature of the image.

**pHYS** -> Holds the pixel size and the ratio of dimensions of the image.

*_Note_* : *_All the ancillary chunks start with a small letter._*

&nbsp;
#### Executable and Linkable Format (ELF):
The ELF file format is standard file format for executables, object codes, core dumps etc. for any UNIX based system.

**Magic Number** -> **7F 45 4c 46**

The file header of an ELF file defines whether to use 32-bit or 64-bit addresses.
ELF files are generally analysed using a tool called **readelf**.

&nbsp;
#### ZIP :
Zip is actually a file format which supports lossless data compression. This file format achieves the compression of a file(s) using a number of compression algorithms.
DEFLATE is the most used compression algorithm. Zip files have the file extension .zip or.ZIP.

 **Magic Number** -> **PK .. ..**
 
![alt text](https://github.com/stuxnet999/Image-Forensics/blob/master/zip.png "ZIP FILE HEADER")

Microsoft Windows, MacOS and several Linux distributions have built-in zip compression.
Zip files can be extracted through the terminal using tools like **binwalk**.
To install binwalk:
```bash
$ sudo apt install binwalk
```
To extract out the compressed data:
``` bash 
$ binwalk -e <file_name>
```
&nbsp;

# Steganography :

#### What is Steganography?
Steganography is an amazing art of hiding data inside images, videos etc. 
The advantage that steganography has over cryptography is that the hidden data does not attract serious attention. However, when someone sees a cryptographic data, they'll immediately recognize that this data is encrypted. Though the extraction of the hidden message is difficult in cryptography, steganographic data looks less malicious!!

### Some known tools for steganography:

**1. Steghide :**

It is used to embed and extract secret messages in images. It supports all the general formats of images like .png, .jpg etc.
##### To install steghide:
```bash
$ sudo apt install stegide
```
##### To embed a secret message into an image:
```bash
$ steghide embed -cf image.jpg -ef secret_message.txt
Enter passphrase : ********
Re-Enter passphrase : ********
embedding "secret_message.txt" in "image.jpg"... done
```
##### To extract secret message from image:
```bash 
$ steghide extract -sf image.jpg
Enter passphrase : ********
wrote extracted data to "secret_message.txt".
```
##### For any help with the commands type:
```bash
$ steghide --help
```
**2. Stegsolve :**

It is used to analyze images in different planes by taking of bits of the image.
##### To install stegsolve:
```bash
$ wget http://www.caesum.com/handbook/Stegsolve.jar -O stegsolve.jar
$ chmod +x stegsolve.jar
$ mkdir bin
$ mv stegsolve.jar bin/
```
Stegsolve can be invoked by placing the image in the /bin folder and running stegsolve. 
```bash
$ java -jar stegsolve.jar
```
![alt text](https://github.com/stuxnet999/Image-Forensics/blob/master/stegsolve-blue.png "The Blue Plane")
![alt text](https://github.com/stuxnet999/Image-Forensics/blob/master/stegsolve-green.png "Green Plane")

There are over 10 different planes supported by stegsolve like **Alpha, Blue, Green, Red, XOR etc**.

**3. Ghex :**
Ghex is tool which helps us to view the hex data or hex dump of an image.
##### To install Ghex:
```bash
$ sudo apt install ghex
```
##### To use Ghex:
```bash
$ ghex image.jpg
```
![alt text](https://github.com/stuxnet999/Image-Forensics/blob/master/ghex.png "Ghex")

Using ghex we can see the headers, footers, and the data chunks of an image.
It is to be noted that ghex can be used for all types of files not only images.
