# parsefixed
Nim module to parse fixed-width fields within lines of text (complementary to parsecsv)

```Nim
import os, parsefixed, streams

var s = newFileStream(paramStr(1), fmRead)
if s == nil: quit("cannot open the file" & paramStr(1))
var x: FwParser
open(x, s, paramStr(1), @[9, 6, 10, 6, 7, 7, 35])
# widths: 9,6,10,... (not starting positions)
while readRow(x):
 echo "new row: "
 for val in items(x.row):
   echo "##", val, "##"
close(x)
```
## Rationale
awk provides two main text processing approaches: regex based field splitting, and fixed-width field splitting.

The Nim pure library, parsecsv, handles non-regex (but delimited) field splitting.

parsefixed is for fixed-width field splitting.

It is line based (terminating in CR, LF, or CR LF), so does not support multi-line field splitting.
