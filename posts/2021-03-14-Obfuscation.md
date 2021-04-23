# Obfuscation - http://challs.dvc.tf:5555/

### Solution

Quick look at its source reveals some obfuscated JavaScript. The most interesting part is '%64%76%43%54%46%7b%31%74%5f%69%73%5f%6e%30%74%5f%34%5f%73%65%63%72%33%74%5f%34%6e%79%6d%30%72%33%7d' because it looks like ASCII.
Let's verify it:

```bash
>>> "".join([chr(int(b, 16)) for b in "%64%76%43%54%46%7b%31%74%5f%69%73%5f%6e%30%74%5f%34%5f%73%65%63%72%33%74%5f%34%6e%79%6d%30%72%33%7d"[1:].split("%")])
'dvCTF{1t_is_n0t_4_secr3t_4nym0r3}'
>>>
```

Yeah, that's it!

### Flag
`dvCTF{1t_is_n0t_4_secr3t_4nym0r3}`

#### Credits

- Writeup by [everl0stz](https://ctftime.org/user/85858)
- Solved by [everl0stz](https://ctftime.org/user/85858)
- WaletSec 2021

#### License

**CC BY 4.0** WaletSec + everl0stz
