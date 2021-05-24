# OpenFSL Documentation

File systems:

| #    | File System Name     | Status          |
| ---- | -------------------- | --------------- |
| 1    | FAT(12/16/32)        | In progress     |
| 2    | VFAT                 | Not Implemented |
| 3    | exFAT                | Not Implemented |
| 4    | NTFS                 | Not Implemented |
| 5    | ext(2/3/4)           | Not Implemented |
| 6    | BtrFS                | Not Implemented |
| 7    | JFS                  | Not Implemented |
| 8    | XFS                  | Not Implemented |
| 9    | ZFS                  | Not Implemented |
| 10   | HFS+                 | Not Implemented |
| 11   | ISO 9660 + El Torito | Not Implemented |
| 12   | UDF                  | Not Implemented |
| 13   | UFS                  | Not Implemented |



## Library Structure

File System

- Logger driver wrapper (inherited from Driver class)
- Disk driver wrapper (inherited from Driver class)
- File system implementation with driver

## Pseudo code for main

```c++
extern Data disk_in(uint64_t offset, size_t sector);
extern int disk_out(uint64_t offset, Data data);

extern int mem_copy(char* dest, char* src, size_t size);

void fsctrl_main() {
    DiskDriver dd = DiskDriver(disk_in, disk_out); // Initialize disk I/O driver
    FS_FAT32 fat32 = FS_FAT32(dd, FAT32_LFN, "/"); // Initialize file system
    
    fat32.start(); // Start file system
    fat32.chdir("::/test1"); // Set directory cursor
    
    FAT32_file file = fat32.openFile("./test2/test3.txt"); // Read file from disk
    
    uint8_t buf[64];
    
    file.read(buf, 64); // Get data from file
    
    file.close(); // Close file
}
```

