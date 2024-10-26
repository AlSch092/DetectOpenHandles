# Detect Open Handles
Code example of detecting open process handles to our process (C/C++, Windows usermode)

![image](https://github.com/AlSch092/DetectOpenHandles/assets/94417808/39a23769-f9b2-4371-a57e-2cec3989f9e5)

## How it works:
- All handles on the system are retrieved via `NtQuerySystemInformation`
- Handles are then filtered based on not being from of the current process (all handles except our current process handles are looked at)
- `DuplicateHandle` is used after `OpenProcess(PROCESS_DUP_HANDLE, FALSE, handle.ProcessId)` to obtain a handle context
- `GetProcessId` on the duplicated handle is then compared to the current process ID, and a match tells us this handle is an open process handle to our process

## Benefits:
- Calls to `OpenProcess` from external applications to our application can be detected

## Drawbacks & Limitations
- Expensive CPU-wise to constantly fetch all handles on the system 
- SERVICE or SYSTEM processes cannot have their handles queried from usermode

Thanks for reading, happy coding!
