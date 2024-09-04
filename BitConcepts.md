so, when you have list of pairs(x,y)  and you want to store it somewhere so that in constant time you can check if x,y is present or not
 1 way. Set<String> st = new HashSet<>();  st.add(x+","+y);

 2. way. Map<Integer, Set<Integer>> mp = new HashMap<>();  mp.computIfAbsent(x, (k)->new HashSet<>()).add(y); // (2,3), (2,4)  => [2 -> [3,4]]
        check  if(mp.containsKey(x)  && mp.get(x).contais(y)){};

3. way  Bit manipulation if x and y are integers that is 32 bit value tahn we can generate 64 bit long value by keeping 
first 32 bit as x and last 32 bit as y

  step 1 =>   ((long)x << 32)  => x converted to long and shifted to first 32 bit
     0xffffffffl = 00...0(32 times) 1111 1111 1111 1111 1111 1111 1111 1111 this is long bit value.
  step 2 => (y & 0xffffffffl)  this will mask the y into long value by keeping first 32 bit same for y;

  step 3 =>  ((long)x << 32) | (y & 0xffffffffl);   this will give single long value whose first 32 bit is x and last 32 bit is y.

 now.. logic time
  for((x,y) : pairs){
    long val = ((long)x << 32) | (y & 0xffffffffl); 
    set.add(val);
  }

  if(set.contains(val)){
    // statement
  }

  -------------------------------------------------------------------------------------------------------------------------------------------





public long encode(int x, int y) {
    return ((long) x << 32) | (y & 0xFFFFFFFFL);
}
 what do you mean by masking y?

 When we talk about "masking" in the context of the expression (y & 0xFFFFFFFFL), we refer to the process of using a bitmask to isolate or modify specific bits in a binary number.

What is Masking?
Masking involves applying a bitwise operation between a number and a bitmask (a number consisting of specific bits set to 1 or 0). The purpose of masking is to preserve certain bits and ignore or modify others.

In the expression (y & 0xFFFFFFFFL), we are using a bitmask 0xFFFFFFFFL to manipulate the 32-bit integer y as part of the process of encoding it into a long.

Breakdown of the Expression (y & 0xFFFFFFFFL)
y:

y is a 32-bit signed integer. This means it can take values from -2,147,483,648 to 2,147,483,647.
When y is converted to a long, which is a 64-bit type, the sign bit of y is extended to fill the upper 32 bits of the long. This is called sign extension.
0xFFFFFFFFL:

0xFFFFFFFFL is a hexadecimal literal representing a 32-bit pattern where all bits are 1. The L at the end ensures it's treated as a long.
In binary, 0xFFFFFFFFL looks like this:
Copy code
00000000 00000000 00000000 00000000 11111111 11111111 11111111 11111111
This bitmask has the lower 32 bits set to 1, and the upper 32 bits set to 0.
Masking with Bitwise AND (&):

The operation (y & 0xFFFFFFFFL) uses the bitwise AND to combine y with the bitmask.
Bitwise AND compares each corresponding bit of the two operands. If both bits are 1, the result is 1; otherwise, it's 0.
Purpose of Masking y
The purpose of the expression (y & 0xFFFFFFFFL) is to mask the sign extension and ensure that y is correctly represented as an unsigned 32-bit integer in the lower 32 bits of the long.

For Positive y:

If y is positive, the upper 32 bits are already 0, so the masking operation doesn't change y.
Example: y = 5
Binary: 00000000 00000000 00000000 00000101
After masking: No change because sign extension doesn't affect positive values.
For Negative y:

If y is negative, sign extension would normally fill the upper 32 bits with 1s when converting to a long.
The mask ensures these upper 32 bits are cleared (set to 0), preserving only the lower 32 bits of y.
Example: y = -2
Binary (int): 11111111 11111111 11111111 11111110
After converting to long without masking: 11111111 11111111 11111111 11111111 11111111 11111111 11111111 11111110
After masking: 00000000 00000000 00000000 00000000 11111111 11111111 11111111 11111110

Summary
The masking operation (y & 0xFFFFFFFFL) ensures that when the 32-bit integer y is converted to a long, only the lower 32 bits of y are preserved, and the upper 32 bits are set to 0. This is crucial for correctly encoding the (x, y) coordinate pair into a single long value without interference from sign extension.

