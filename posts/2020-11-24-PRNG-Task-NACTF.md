# PRNG Task

### Solution

There are two ways to predict next numbers Mersenne Twister returns.
The first is rebuilding its internal state using 624 integers. The second way is guessing the seed and guessing it shouldn't be that hard, because source code we get tells us it's rounded time.

Code:

```python
import socket
import time
import random
import math
import datetime

HOST = "challenges.ctfd.io"
PORT = 30264

def main():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    my_tm = round(time.time() / 100, 5)
    s.connect((HOST, PORT))
    srv_nums = []
    print("current time: %f" % my_tm)

    recvd = s.recv(4096).decode("UTF-8")
    while True:
        if len(srv_nums) != 2:
            s.sendall(b"r\n")
            recvd = s.recv(128).decode("UTF-8")
            recvd = recvd[:recvd.find("\n")]
            srv_nums.append(int(recvd))
            continue
            break

    print("bruteforcing seed")
    print("searching for numbers:", srv_nums)
    flag_found = False
    print("displaying progress...\n")
    work_begin = time.time()

    my_tm = round(my_tm - 30, 6)
    while True:
        random.seed(my_tm)
        my_rnd = random.randint(1, 100000000)
        if my_rnd == srv_nums[0]:
            print("found time seed: %f" % my_tm)
            tmprng = random.randint(1, 100000000)
            print(tmprng)
            if tmprng != srv_nums[1]:
                print("second number doesn't match, skipping")
                my_tm = round(my_tm + 0.000001, 6)
                continue
            flag_found = True
            break
        my_tm = round(my_tm + 0.000001, 6)
        if my_tm == float(math.floor(my_tm)):
            print(int(my_tm))
                work_end = time.time()
    print("finished job in %s" % str(datetime.timedelta(seconds=work_end - work_begin)))

    if not flag_found:
        print("seed not found")
        return

    print("\nsubmitting the answer")
    print("\nserver numbers")
    for x in srv_nums:
        print("| %i |" % x, end="")

    print("")
    s.sendall(b"g\n");

    first_rnd = random.randint(1, 100000000)
    recvd = s.recv(4096)
    print(recvd)
    s.sendall(str(first_rnd).encode("utf-8") + b"\n")
    print("sent first guess: %i" % first_rnd)

    second_rnd = random.randint(1, 100000000)
    recvd = s.recv(4096)
    print(recvd)
    s.sendall(str(second_rnd).encode("utf-8") + b"\n")
    print("sent second guess: %i" % second_rnd)

    while True:
        recvd = s.recv(4096).decode("utf-8")
        if not recvd:
            break
        print(recvd)

if __name__ == "__main__":
    main()
```

We run it and get the flag:

```python
found time seed: 16045235.553690
95870824
finished job in 0:03:57.809325

submitting the answer

server numbers
| 71504180 || 95870824 |
b'Guess the next two random numbers for a flag!\nGood luck!\nEnter your first guess:\n> '
sent first guess: 94324429
b"Wow, lucky guess... You won't be able to guess right a second time\nEnter your second guess:\n> "
sent second guess: 68431170
What? You must have psychic powers... Well here's your flag: 
nactf{ch000nky_turn1ps_1674973}
```

### Flag

​	nactf{ch000nky_turn1ps_1674973}

#### Credits

- Writeup by [everl0stz](https://ctftime.org/user/85858)
- Solved by [everl0stz](https://ctftime.org/user/85858)
- WaletSec 2020

#### License

**CC BY** WaletSec + everl0stz
