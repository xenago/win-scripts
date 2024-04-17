# ie

Control Internet Explorer.

## Useful commands:

Batch command to open IE post-removal:

    @PowerShell -ExecutionPolicy RemoteSigned -Command New-Object -COMObject InternetExplorer.Application -Property @{Navigate2='https://github.com'; Visible=1}

