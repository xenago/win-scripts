# cmd

CMD/batch scripts and utilities.

# Repeatedly run command

This will run `echo test` command every 2 seconds:

    for /l %g in () do @( echo test & timeout /t 2 )
