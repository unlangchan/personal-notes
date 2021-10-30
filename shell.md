常用打包形式(mac排除系统目录文件)
```
tar --exclude '.DS_Store' --exclude '__MACOSX' -czf xx-$(date +%Y%m%d%H%M).tar.gz xx
```