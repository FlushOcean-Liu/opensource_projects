# mbuf详解

## headroom和tailroom作用
网卡收包后需要对报文进行解析，这个解析一般时一次性的，后续报文继续流动，在其他模块、进程中  
存在使用前面预先解析的结果，这时如果重新解析会导致重复处理，延迟收包速度。

此时mbuf的headroom与tailroom就派上用场，每个mubf的headroom大小与tailroom的大小在创建的时候就已经确定，
后续可以将解析报文关键信息存储到headroom或tailroom中，其他模块、进程在获取到mubf后，通过增加相应的偏移就能
获取到已经解析过字段值。