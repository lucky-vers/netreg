# netreg

Just something I cooked up at 2AM with ChatGPT. Predicts when iBus decides to shit itself for no reason with 76% accuracy. Will do this with a bit more data next time (promise).

Here's the shell script I ran as a cronjob every minute to collect data

```sh
#!/bin/sh

if ! nmcli connection show | head -2 | grep 'Block-6'
then
    echo "$(date +%s),off" >> "$HOME/.cache/nstat"
    exit 0
fi

if ping -c 1 google.com >/dev/null 2>&1
then echo "$(date +%s),on"  >> "$HOME/.cache/nstat"
else echo "$(date +%s),off" >> "$HOME/.cache/nstat"
fi
```
