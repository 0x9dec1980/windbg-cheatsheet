# Windbg cheatsheet


### VirtualKD + WinDbgX.exe preview

#### Set custom debugger to:

```ruby
C:\Users\<user>\AppData\Local\Microsoft\WindowsApps\WinDbgX.exe /k com:pipe,resets=0,reconnect,port=$(pipename)
```

### Symbols

#### Configure symbol cache & MS symbol server

```ruby
!sympath srv*c:\symbols*https://msdl.microsoft.com/download/symbols
```
#### Load unloaded driver PDB

```ruby
.reload /unl foo.sys
```


### Conditional breakpoints

#### Break if caller module is X

Example: break in nt!FsRtlCreateSectionForDataScan when called from within Sysmon driver: 

```ruby
bp nt!FsRtlCreateSectionForDataScan "r $t0 = 0; .foreach ( v { k }) { .if ($spat(\"v\", \"*SysmonDrv*\"))  { r $t0 = 1; .break } }; .if($t0 = 0) { gc }"
```

### Resolve stack pointers

#### x86
```
dps esp - 3000 esp + 3000
```
#### x64
```
dps esp - 4000 esp + 4000
```

### Displays the full parameters for all stacks, as well as stacks that are currently paged out and the current kernel stacks.
```
!stacks 2
```

### Ring3 breakpoints in a remote kernel debug session

Example: Switch context to target process to be debugged invasively, set a breakpoint for this process and force pagein of virtual address if needed.

```ruby
.process /i fffffa80038b8060
.cache forcedecodeuser
bp /p fffffa80038b8060 ntdll!ntcreatefile
.pagein fffffa80038b8060 7fefcc9e100
```







 
