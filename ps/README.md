# ps

PowerShell commands and utilities.

# Repeatedly run command

Every 180 seconds, this will print the date and then run a command:

while (1) {date -format s; MYCOMMANDHERE; sleep 180}

