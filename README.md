# BytesTable

_Visualizing byte arrays_

Bytes Tables provides a module that pretty print byte arrays like you know from many tools, like hex editors, Wireshark and the likes. It is intended to support during the development of components handling byte arrays, like a DNS client or server. Typically byte arrays are printed to the FSI like this:
```fs
val bytes : byte [] =
  [|200uy; 211uy; 163uy; 6uy; 77uy; 222uy; 200uy; 247uy; 51uy; 51uy; 138uy;
    76uy; 8uy; 0uy; 69uy; 0uy; 0uy; 55uy; 163uy; 217uy; 0uy; 0uy; 128uy; 17uy;
    21uy; 20uy; 192uy; 168uy; 0uy; 119uy; 192uy; 168uy; 0uy; 1uy; 202uy; 30uy;
    0uy; 53uy; 0uy; 35uy; 76uy; 151uy; 189uy; 72uy; 1uy; 0uy; 0uy; 1uy; 0uy;
    0uy; 0uy; 0uy; 0uy; 0uy; 6uy; 103uy; 111uy; 111uy; 103uy; 108uy; 101uy;
    2uy; 100uy; 101uy; 0uy; 0uy; 1uy; 0uy; 1uy|]
```

which is no so much informative. Byte Tables adds a formatter to show this byte array like this:
```
0000    c8 d3 a3 06 4d de c8 f7 33  33 8a 4c 08 00 45 00    ····M···33·L··E·
0010    00 37 a3 d9 00 00 80 11 15  14 c0 a8 00 77 c0 a8    ·7···········w··
0020    00 01 ca 1e 00 35 00 23 4c  97 bd 48 01 00 00 01    ·····5·#L··H····
0030    00 00 00 00 00 00 06 67 6f  6f 67 6c 65 02 64 65    ·······google·de
0040    00 00 01 00 01
```

## Usage

For Scripts, you can just download the `BytesTable.fsx` file, load it in your script and add an FSI printer for it.
```fs
#load @"paket-files\ChrSteinert\BytesTable\BytesTable.fsx"

open BytesTable

fsi.AddPrinter BytesTable.getBytesTable

let bytes = 
    "yNOjBk3eyPczM4pMCABFAAA3o9kAAIARFRTAqAB3wKgAAcoeADUAI0yXvUgBAAABAAAAAAAABmdvb2dsZQJkZQAAAQAB" // A TCP frame of a DNS request for the address of 'google.de'
    |> System.Convert.FromBase64String

bytes // prints the following:
// 0000    c8 d3 a3 06 4d de c8 f7 33  33 8a 4c 08 00 45 00    ····M···33·L··E·
// 0010    00 37 a3 d9 00 00 80 11 15  14 c0 a8 00 77 c0 a8    ·7···········w··
// 0020    00 01 ca 1e 00 35 00 23 4c  97 bd 48 01 00 00 01    ·····5·#L··H····
// 0030    00 00 00 00 00 00 06 67 6f  6f 67 6c 65 02 64 65    ·······google·de
// 0040    00 00 01 00 01
```