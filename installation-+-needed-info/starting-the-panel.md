# Starting the Panel

## Testing \(Step 1\)

To test that Astu Panel works, type the commands below.

```text
cd astupanel
node index.js

# Your output should send the following message (Your port may be different)
# [WEBSITE] The dashboard successfully loaded on port 80.
```

If you did not receive the message on the last line, ask help on our discord! [https://astuhosting.com/discord](https://astuhosting.com/discord)

{% hint style="warning" %}
Cancel the process by pressing CTRL C before moving on to Step 2
{% endhint %}

## Production \(Step 2\)

Now that we know everything's running smoothly, we can ensure that the panel is always up. even after leaving your SSH session!  


```text
npm install pm2 -g
pm2 start index.js
```

You are now good to go! Have fun on your endeavors!!!

