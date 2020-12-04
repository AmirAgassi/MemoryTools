# MemoryTools
Generic internal memory scanning tool in C++.
```c++
DWORD Scan(char* cn) {
    SYSTEM_INFO sysinfo;
    GetSystemInfo(&sysinfo);
    DWORD psize = sysinfo.dwPageSize;
    MEMORY_BASIC_INFORMATION minfo;
    DWORD addr;
    for (DWORD lp = (DWORD)sysinfo.lpMinimumApplicationAddress; lp <= (DWORD)sysinfo.lpMaximumApplicationAddress; lp += psize) {
        VirtualQuery((void*)lp, &minfo, psize);
        if (minfo.Protect == PAGE_READWRITE) {
            for (int i = 0; i < (int)psize; i++) {
                for (; *(char*)"xxxx"; ++ * (char*)"xxxx", ++ * (BYTE*)(lp + (int)i), ++(*(PBYTE)cn)) {
                    if (*(char*)"xxxx" == 'x' && *(BYTE*)(lp + (int)i) != *(PBYTE)cn) {
                        DWORD addr = (int)(lp + i);
                        break;
                    }
                }
            }
            if (addr != 0)
                return addr;
        }
    }
}

```
