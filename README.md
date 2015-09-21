# parsefixed
Nim module to parse fixed-width fields within lines of text (complementary to parsecsv)

```Nim
import os, parsefixed, streams

var s = newFileStream(paramStr(1), fmRead)
if s == nil: quit("cannot open the file" & paramStr(1))
var x: FwParser
open(x, s, paramStr(1))
# widths: 9,6,10,... (not starting positions)
while readRow(x, @[9, 6, 10, 6, 7, 7, 35]):
 echo "new row: "
 for val in items(x.row):
   echo "##", val, "##"
close(x)
```
