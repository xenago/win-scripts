# partition

Partitioning disks with Windows.

## Moving EFI partition

For example, use a second small disk to hold the EFI and the primary to hold the recovery and `C:` partitions.

**IMPORTANT: back up the disk with a snapshot at minimum before proceeding, this is easy to screw up**

1. Add disk to VM (200MB is enough, EFI only needs 100MB usually)

2. Reboot Windows into Recovery mode by logging in, hitting Start, and then holding Shift while using the Restart option

3. Open the recovery command line as the Administrator account

4. Set up the new disk as GPT with EFI partition assigned a letter (it will not have a letter once Windows boots)

       diskpart
       list vol                    (confirm the Windows drive letter, and find an unused one to use temporarily)
       list disk                   (find the number of the new disk)
       sel disk 99                 (use the number of the new disk)
       clean
       convert gpt
       create partition efi
       format fs=fat32 label="EFI"
       assign letter=v             (this will be a temporarily-assigned letter)
       exit

5. Create the EFI boot data, using the Windows drive letter and temporary drive letter from the previous step

       bcdboot C:\Windows /s V: /f UEFI

6. Delete the old efi partition (be careful to select the system EFI partition and not the data or recovery partitions!)

       diskpart
       list disk          (locate the disk number Windows is installed on originally, which has the original now-obsolete EFI partition)
       sel disk 99        (select the Windows disk)
       list part          (locate the EFI partition number)
       sel part 99        (select the EFI partition number)
       del part override  (override is required to bypass restriction on deleting system data)
       list part          (notice the EFI partition is removed)
       
8. Reboot system to confirm it works
