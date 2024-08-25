# Overview 


The byte-order mark (BOM) is a particular usage of the special Unicode character code, U+FEFF ZERO WIDTH NO-BREAK SPACE, whose appearance as a magic number at the start of a text stream can signal several things to a program reading the text:[1]

- the byte order, or endianness, of the text stream in the cases of 16-bit and 32-bit encodings;
- the fact that the text stream's encoding is Unicode, to a high level of confidence;
- which Unicode character encoding is used.

BOM use is optional. Its presence interferes with the use of UTF-8 by software that does not expect non-ASCII bytes at the start of a file but that could otherwise handle the text stream.

Unicode can be encoded in units of 8-bit, 16-bit, or 32-bit integers. For the 16- and 32-bit representations, a computer receiving text from arbitrary sources needs to know which byte order the integers are encoded in. The BOM is encoded in the same scheme as the rest of the document and becomes a noncharacter Unicode code point if its bytes are swapped. Hence, the process accessing the text can examine these first few bytes to determine the endianness, without requiring some contract or metadata outside of the text stream itself. Generally the receiving computer will swap the bytes to its own endianness, if necessary, and would no longer need the BOM for processing.

The byte sequence of the BOM differs per Unicode encoding (including ones outside the Unicode standard such as UTF-7, see table below), and none of the sequences is likely to appear at the start of text streams stored in other encodings. Therefore, placing an encoded BOM at the start of a text stream can indicate that the text is Unicode and identify the encoding scheme used. This use of the BOM is called a "Unicode signature".[2]

