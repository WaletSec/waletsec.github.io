# The Matrix | Web

### Solution

From ctf we have got website ip
> `http://chals5.umdctf.io:4000`

Only interesting thing on website was **/the-matrix** subpage that redirects to **/403** where we could see this message

> This page is for robots only, you are not allowed to access this content!

This message gave me a hint that with *Google Bot User Agent* I should be able to see the real content of **/the-matrix** page

> `curl -A 'Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)' http://chals5.umdctf.io:4000/the-matrix`

Using this command ends up with a flag

### Flag

UMDCTF-{r0b0t_r3b3ll!0n}

#### Credits

- Writeup by [HuntClauss](https://ctftime.org/user/106464)
- Solved by [HuntClauss](https://ctftime.org/user/106464)
- WaletSec 2021

#### License

**CC BY 4.0** WaletSec + HuntClauss
