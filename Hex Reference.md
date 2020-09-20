
```
0000000 aabb ccdd eeff 0011 2233 4455 6677 8899
0000010 ...

1 byte = F0
1 word = FF00
1 row = 16 bytes
32 rows = 512 bytes
256 rows = 4096 bytes (16x16x16 bytes)

512 bytes: ____000 -> ____1ff

1st Block: 0000000 -> 0000fff
2nd Block: 0001000 -> 0001fff
3rd Block: 0002000 -> 0002fff
...
```
