
the difference between `Int(20)` and `BigInt(20)` in mysql:

an `Int` is 4 bytes signed number, and a `BigInt` is 8 bytes signed number.

the number 20 does only affect the display width of the column, but not the storage.

Relational algebra is based on sets (unordered, no duplicates). SQL is based on bags (unordered,
allows duplicates).