# Windbg cheatsheet

```ruby
bp nt!FsRtlCreateSectionForDataScan "r $t0 = 0; .foreach ( v { k }) { .if ($spat(\"v\", \"*SysmonDrv*\"))  { r $t0 = 1; .break } }; .if($t0 = 0) { gc }"
```



 
