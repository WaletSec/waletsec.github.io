# World Trip

### Solution

We get coordinates in format (longitude, latitude)(longitude, latitude)(long, lat) etc...
Here is my Python script I used to get the flag from first characters of every country names:

```python
from geopy.geocoders import Nominatim

gl = Nominatim(user_agent="Some random user agent")

with open("longlat.txt", "r") as f:
  crds = f.read().strip().replace(")(", ")\n(").split("\n")

flag = ""
for crd in crds:
  lat, long = crd.replace("(", "").replace(")", "").split(",")
  lat = float(lat)
  long = float(long)

  loc = gl.reverse([lat, long], language="en")
  flag += loc.raw["address"]["country"][0]

print(flag)
```

### Flag

​	nactf{IHOPEYOUENJOYEDGOINGONTHATREALLYLONGGLOBALTOURIBOFAIQFUSETZOROPZNQTLENFLFSEMOGMHDBEEIZOIUOCGSLCDYMQYIRLBZKNHHFGBPDIVNBUQQYPDCQIAVDYTRFOCESEQUOUUMSKYJOVKVJGMRGNATNIRESHRKHCEDHHZYQRZVOGCHSBAYUBTRU}

#### Credits

- Writeup by [everl0stz](https://ctftime.org/user/85858)
- Solved by [everl0stz](https://ctftime.org/user/85858)
- WaletSec 2020

#### License

**CC BY 4.0** WaletSec + everl0stz
