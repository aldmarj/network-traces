# Analyzing a Netsh Trace with Wireshark

Windows ships with an inbox packet capture component called ndiscap. 
A capture can be collected using netsh within an elevated CMD prompt:

```
netsh trace start capture=yes tracefile=c:\nettrace-boot.etl persistent=yes maxsize=4096
 
<Reproduce the issue>

netsh trace stop
```

Netsh outputs a .etl file; to analyze the trace in Wireshark, the .etl file will need to be converted to a .cap file. The tool etl2pcapng  will generate a .cap file from an .etl file.

More information and prebuilt binaries are available here:
https://github.com/microsoft/etl2pcapng

Within the same directory as the executable, run the following command to perform the conversion.

```
etl2pcapng.exe nettrace-boot.etl test.cap
```

Note, .etl files can be analyzed using Microsoft Network Monitor, Microsoft Message Analyzer and PerfView. However, I have found Wireshark to be the most intuitive.
