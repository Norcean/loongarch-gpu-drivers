# instruction

install loongarch gpu drivers for new world on archlinux.

You may need to use the following method to disable the `loongson` module.

```bash
echo -e "blacklist loongson" > /etc/modprobe.d/blacklist-loongson.conf
```
