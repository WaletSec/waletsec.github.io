# P*rn protocol solution

### You will need

- Python3
- Challenge files

We get server address and protocol specification.
The specs says that our messages must be "prefixed" with message ID and session ID.
Server allows 4 message exchanges, that should be enough for us to get the flag.

Here is the script I used to get the flag (with comments)

⚠ Warning: the code is really bad and full of ugly hacks

```python
import socket

def typetodescr(t):
    if t == 0x01:    return "message id"
    elif t == 0x02:    return "identifier"
    elif t == 0x03: return "member id"
    elif t == 0x04: return "login"
    elif t == 0x05: return "flag"
    elif t == 0xff: return "error"
    else:    return "unknown"

def deserialize(d):
    psz = d.pop(0)        # the first byte is size of message
    ptype = d.pop(0)    # second byte - message type
    pcontent = []            # next psz - 1 - actual content
    for i in range(0, psz - 1):
        pcontent.append(d.pop(0))
    return d, psz, ptype, pcontent

def serialize(ptype, pcontent):
    buf = []
    psz = len(pcontent) + 1
    buf.append(psz)
    buf.append(ptype)
    buf.extend(pcontent)
    return bytes(buf)

def auth_send(s, sid, xchg_num, packet):    # prefix packets with authentication
    msg_id = serialize(0x01, [xchg_num])
    identifier = serialize(0x02, sid)
    s.sendall(msg_id + identifier + packet)
    return xchg_num + 1

def main():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("flu.xxx", 2005))
                print("got xchg_num:", pcontent[0])
                xchg_num = pcontent[0] # gonna be xchg_num + 1
            elif ptype == 0x02:
                sid = pcontent
                print("got session id:", bytes(sid))
            elif ptype == 0x03 and pcontent[0] == 0x01:
                print("")
                print("authenticating and requesting new user credentials")
                xchg_num = auth_send(s, sid, xchg_num, serialize(0x03, [0x02]))
            elif ptype == 0x03 and pcontent[0] == 0x03:
                username = "".join([chr(x) for x in pcontent[1:]])
                print("got username:", username)
            elif ptype == 0x03 and pcontent[0] == 0x04:
                password = "".join([chr(x) for x in pcontent[1:]])
                print("got password:", password)

                print("logging in")
                auth_send(s, sid, xchg_num, serialize(0x04, [0x01]))
            elif ptype == 0x04 and pcontent[0] == 0x02:
                print("logged in successfully")
                print("requesting flag...")
                auth_send(s, sid, xchg_num, serialize(0x05, [0x01]))
            elif ptype == 0x05:
                print("got the flag, woohoo!!!")
                flag = "".join([chr(x) for x in pcontent]) # forgive me
                print("and the flag is: '%s'" % flag)
                print("well done, closing connection.")
                s.shutdown(socket.SHUT_RDWR)
                s.close()
                return
            elif ptype == 0xff:
                print("[!] error: %s, closing connection" % hex(pcontent[0]))
                return
            else:
                print("[?] unknown packet type, that's a weird one")
                return
            print("---------------------------")

if __name__ == "__main__":
    main()
```

### Flag

​	flag{**vpns_ar3_n0t_h4ck3r_appr0v3d**}

#### Credits

- Writeup by [everl0stz](https://ctftime.org/user/85858)
- Solved by [everl0stz](https://ctftime.org/user/85858)
- WaletSec 2020

#### License

**CC BY 4.0** WaletSec + everl0stz