# BearcatCTF 2025 World Tour

## Shimbles-the-elf
```c=
int __fastcall main(int argc, const char **argv, const char **envp)
{
  if ( fgets(s1, 128, stdin) )
  {
    .......
    if ( !strcmp(s1, s2) )
    {
      v5 = strlen(v9);
      two_layer_decrypt(v9, v5, 119LL, 4LL, 60LL, 3LL);
      puts("\nSchimbles: Ha! You have bested me!");
      printf("Schimbles: Here is your flag: %s\n", v9);
    }
    ......
  }
........
}
```
I just need to run the debugger to check the value of `s2`
And the decryption key is `elfmagic`
![image](https://hackmd.io/_uploads/BJn1ZT1FJg.png)
`flag: BCC{n0t_t0day_e1f}`
## Easy Encrypt
```python=
enc = [0x73, 0x70, 0x70, 0x63, 0x77, 0x48, 0x04, 0x7F, 0x05, 0x04, 
  0x6C, 0x40, 0x05, 0x40, 0x5D, 0x43, 0x6E, 0x40, 0x03, 0x68, 
  0x79, 0x07, 0x41, 0x73, 0x4c]

key = [0x31, 0x33, 0x33, 0x37]
from pwn import *
print(xor(enc, key))
```
`flag: BCCTF{7H47_w4snt_s0_H4rD}`

## Crython
The condition is that after a series of calculations, the final value must be equal to
`14154190239817593391562602231552196407925674789718962804833972736086242830332675315723974651`
So, I use Z3 to solve this challenge
**For convenience, you should edit them using Notepad**

```python=
from z3 import *
s = Solver()
bit_size = int(input("bit_size: "))
f = BitVec('f', bit)
s.add(.....) #Fill in the entire expression
# Because the expression is quite large, it cannot be contained here
if s.check() == sat:
	m = s.model()
	print(m[f].as_long().to_bytes(bit_size//8, 'big'))
else:
	print("No solution")
```
I tried values from 128 to 512, and the result I received was:
![image](https://hackmd.io/_uploads/HJEnt21F1e.png)
`flag: BCCTF{D0n7_cry_175_4LL_g01n6_t0_b3_0K}`