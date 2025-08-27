# ps

PowerShell commands and utilities.

# Repeatedly run command

Every 2 seconds, this will print the date and then run a command, similar in effect to `watch -n 2 'echo test'`:

    while (1) {date -format s; echo test; sleep 2}
