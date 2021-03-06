# uvarint
[![Build Status](https://travis-ci.org/mohae/uvarint.png)](https://travis-ci.org/mohae/uvarint)  

Varint is SQLite4's variable-length integers: an encoding of 64-bit unsigned integers into between 1 and 9 bytes.

The Encode and Decode functions, `PutUvarint` and `Uvarint`, respectively, also document the rules for encoding/decoding as documented on http://www.sqlite.org/src4/doc/trunk/www/varint.wiki.  The rules are copied directly from that page.

For more information about SQLite4's varint, please refer to the above link.

When encoding, the passed byte slice must be have a len of _n_ bytes where _n_ is the number of bytes that the number will encode to, up to a max of 9 bytes.  A panic will occur if the byte slice is not long enough to hold the encoded number.  The number to encode must be of type `uint64`.  The number of bytes encoded will be returned.

Uint64 takes a byte slice and returns the decoded number as a `uint64` and the number of bytes read.  A panic will occur if the byte slice length is less than expected.  The expected length is determined by the value of the first byte.

## Usage

    package main

    import "github.com/mohae/uvarint"

    func main() {
            buf := make([]byte, 9)
            n := uvarint.PutUvarint(buf, 42)
            fmt.Printf("Encoded %d bytes: %#v\n", buf)

            v, n := uvarint.Uvarint(buf)
            fmt.Printf("Decoded %d bytes: %d\n", n, v)
    }

Output:

    Encoded 1 bytes: 0x2a
    Decoded 1 bytes: 42

## Notes:
Two wrapper functions are also exposed:  `Encode` and `Decode`.  `Encode` is a wrapper to `PutUvarint`, while `Decode` wraps `Uvarint`.

## Doc  
https://godoc.org/github.com/mohae/uvarint
