
##### Luau binary format
|Description          |Type                |
|---------------------|--------------------|
|Version              |Byte                |
|Strings Table Size   |VarInt              |
|    … String         |                    |
|        String Length|VarInt              |
|        String       |Char array          |
|Function Table Size  |VarInt              |
|… Function           |(See function table)|
|Main function        |VarInt              |

##### Function
|Description          |Type                |
|---------------------|--------------------|
|Max stack size       |Byte                |
|Number params        |Byte                |
|Number upvalues      |Byte                |
|Is vararg            |Byte                |
|Instruction count    |Byte                |
|… Bytecode           |Array of bytes      |
|Constants count      |VarInt              |
|… Constant           |                    |
|    Constant type    |Byte                |
|    Data             |(See the constant types table for potential data)|
|Child Proto Count    |VarInt              |
|… Proto              |VarInt              |
|Debug line defined   |VarInt (If Version is 2, this is set)|
|Debug name           |VarInt              |
|Has lines            |Byte                |
|    Line Info        |LineInfo (Only present if Has lines == 1 )|
|Has debug            |Byte (Extra data onlky present if == 1)|
|    Debug local count|VarInt              |
|    … DebugLocal     |DebugLocal          |
|    Debug upvalue count|VarInt              |
|        … Upvalue name|VarInt              |

##### Constant Type
|Description          |Type                |Extra Info                      |
|---------------------|--------------------|--------------------------------|
|Nil                  |                    |                                |
|No data              |                    |                                |
|Boolean              |                    |                                |
|    Value            |Boolean             |                                |
|Number               |                    |                                |
|    Value            |Double              |                                |
|String               |                    |                                |
|    Value            |VarInt              |Index into string table         |
|Import               |                    |                                |
|    Value            |Int                 |10-10-10-2 encoded import id?   |
|Table                |                    |                                |
|    Shape Length     |VarInt              |                                |
|    … Shape Keys     |VarInt              |                                |
|Closure              |                    |                                |
|    Function Index   |VarInt              |Index of function in global list|

##### Debug Local
|Description          |Type                |Extra info                      |
|---------------------|--------------------|--------------------------------|
|Name                 |VarInt              |Index to strings table?         |
|StartPC              |VarInt              |                                |
|EndPC                |VarInt              |                                |
|Register             |Byte                |                                |

##### Line Info
|Description          |Type                |
|---------------------|--------------------|
|logspan              |Byte                |
|    … lastOffset     |Byte                |
|    … lastLine       |Int                 |
