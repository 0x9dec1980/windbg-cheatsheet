# Windbg cheatsheet

## Conditional breakpoints

### Break if caller module is X

Example: break in nt!FsRtlCreateSectionForDataScan when called from within Sysmon driver: 

```ruby
bp nt!FsRtlCreateSectionForDataScan "r $t0 = 0; .foreach ( v { k }) { .if ($spat(\"v\", \"*SysmonDrv*\"))  { r $t0 = 1; .break } }; .if($t0 = 0) { gc }"
```



 
