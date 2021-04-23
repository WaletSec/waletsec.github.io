# Zip Madness

### Solution

We get file named flag.zip. After unpacking it, it seems like we have to unpack 1000 other ZIPs depending on direction specified in direction.txt
I used simple bash script to do it:

```bash
for i in {1000..1}
do
  `unzip -o $i$(cat direction.txt).zip`
done
```
### Flag

​	nactf{1_h0pe_y0u_d1dnt_d0_th4t_by_h4nd_87ce45b0}

#### Credits

- Writeup by [everl0stz](https://ctftime.org/user/85858)
- Solved by [everl0stz](https://ctftime.org/user/85858)
- WaletSec 2020

#### License

**CC BY 4.0** WaletSec + everl0stz
