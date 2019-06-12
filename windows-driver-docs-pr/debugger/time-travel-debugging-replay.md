---
title: 时光穿越调试 - 重放跟踪
description: 本部分介绍如何重播时间旅行跟踪。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4f9eb21ef930c66b3995e4afbd587a347049b880
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364775"
---
![显示时钟的较短时间的行程徽标](images/ttd-time-travel-debugging-logo.png) 

# <a name="time-travel-debugging---replay-a-trace"></a>时光穿越调试 - 重放跟踪 

本部分介绍如何重播按时间顺序查看跟踪，向前导航和向后的时间。

## <a name="command-time-travel-navigation"></a>命令时间旅行导航

使用以下命令使用尾随负号在过去。

| Command  | 
|----------------|
| p-（后退） | 
| t-（回溯）| 
| g-（返回）   |

有关详细信息，请参阅[时间旅行调试-导航命令](time-travel-debugging-navigation-commands.md)。 

## <a name="ribbon-button-time-travel-navigation"></a>功能区按钮时间旅行导航

或者，使用功能区按钮在跟踪中导航。

![显示开始录制复选框的 WinDbg 预览的屏幕截图](images/ttd-ribbon-buttons.png)


## <a name="example-ttd-trace-replay"></a>示例 TTD 跟踪重播

使用 g 命令来执行向后直到事件或达到 TTD 跟踪的开头。 可以停止向后执行的事件都将停止向前执行相同。 在此示例中，达到了跟踪的开始。


```dbgcmd
0:000> g-
TTD: Start of trace reached.
(3f78.4274): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 29:0
ntdll!ZwTestAlert+0x14:
00007ffc`61f789d4 c3              ret
```

使用[p （步骤）](https://docs.microsoft.com/windows-hardware/drivers/debugger/p--step-)命令来单步前进 TTD 跟踪中。 

```dbgcmd
0:000> p
Time Travel Position: F:1
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774f828 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x1bc5:
7774f828 740b            je      ntdll!LdrpInitializeProcess+0x1bd2 (7774f835) [br=1]
0:000> p
Time Travel Position: F:2
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774f835 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x1bd2:
7774f835 83bdd0feffff00  cmp     dword ptr [ebp-130h],0 ss:002b:010ff454=00000000
0:000> p
Time Travel Position: F:3
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774f83c esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x1bd9:
7774f83c 0f8450e8ffff    je      ntdll!LdrpInitializeProcess+0x42f (7774e092) [br=1]
```

你还使用[t (Trace)](https://docs.microsoft.com/windows-hardware/drivers/debugger/t--trace-)命令在跟踪中导航。

```dbgcmd
0:000> t
Time Travel Position: F:4
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774e092 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x42f:
7774e092 33c0            xor     eax,eax
0:000> t
Time Travel Position: F:5
eax=00000000 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774e094 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x431:
7774e094 e9f5170000      jmp     ntdll!LdrpInitializeProcess+0x1c2b (7774f88e)
```


使用 p 命令 TTD 跟踪中向后步骤。 

```dbgcmd
0:000> p-
Time Travel Position: F:4
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774e092 esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x42f:
7774e092 33c0            xor     eax,eax
0:000> p-
Time Travel Position: F:3
eax=0173a5b0 ebx=00fd8000 ecx=7774f821 edx=0f994afc esi=0f99137c edi=00de0000
eip=7774f83c esp=010ff34c ebp=010ff584 iopl=0         nv up ei pl zr na pe nc
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000246
ntdll!LdrpInitializeProcess+0x1bd9:
7774f83c 0f8450e8ffff    je      ntdll!LdrpInitializeProcess+0x42f (7774e092) [br=1]
```

T 命令还可用于在时间中向后导航。


## <a name="tt-navigation-commands"></a>！ tt 导航命令

使用 ！ tt 命令向前或向后导航通过跳过到在跟踪中的给定位置中的时间。 

！ tt [位置]

提供在任何时间传输到该点的以下格式的时间位置。
           
- 如果 [位置] 是介于 0 和 100 之间的十进制数字，它跟踪到传输大约该 %。 例如`!tt 50`传输到中途跟踪。

- 如果 {位置} #: #，其中 # 为十六进制数字，它传递到该位置。 例如，`!tt 1A0:12F`方式传送 1A0:12F 定位在跟踪中。

有关详细信息，请参阅[调试旅行时间-！ tt （时程）](time-travel-debugging-extension-tt.md)。


## <a name="positions"></a>！ 位置

使用`!positions`以显示所有活动的线程，包括在跟踪中的位置。 有关详细信息，请参阅[调试旅行时间-！ 位置 （时程）](time-travel-debugging-extension-positions.md)。

```dbgcmd
0:000> !positions
>Thread ID=0x1C74 - Position: F:2
 Thread ID=0x1750 - Position: A5:0
 Thread ID=0x3FFC - Position: 200:0
 Thread ID=0x36B8 - Position: 403:0
 Thread ID=0x3BC4 - Position: 5F2:0
 Thread ID=0x392C - Position: B45:0
 Thread ID=0x32B4 - Position: C87:0
 Thread ID=0x337C - Position: DF1:0
```
此示例演示在当前位置有八个线程。 当前线程是 3604，标有 >。  

> [!TIP] 
> 若要显示当前的线程和它们的位置列表的另一种方法是使用数据模型 dx 命令：
>
> `dx -g @$curprocess.Threads.Select(t => new { IsCurrent = t.Id == @$curthread.Id, ThreadId = t.Id, Position = t.TTD.Position })`
>

使用用户模式[~ （线程状态）](---thread-status-.md)命令显示了相同的八个线程，并将标记与当前线程。:

```dbgcmd
0:000> ~
.  0  Id: 954.1c74 Suspend: 4096 Teb: 00fdb000 Unfrozen
   1  Id: 954.1750 Suspend: 4096 Teb: 00fea000 Unfrozen
   2  Id: 954.3ffc Suspend: 4096 Teb: 00fde000 Unfrozen
   3  Id: 954.36b8 Suspend: 4096 Teb: 00fe1000 Unfrozen
   4  Id: 954.3bc4 Suspend: 4096 Teb: 00fe4000 Unfrozen
   5  Id: 954.392c Suspend: 4096 Teb: 00fed000 Unfrozen
   6  Id: 954.32b4 Suspend: 4096 Teb: 00ff0000 Unfrozen
   7  Id: 954.337c Suspend: 4096 Teb: 00ff3000 Unfrozen
```

单击中的第三个线程 (3FFC) 旁边的链接 ！ 定位输出到跟踪 200:0 中该位置按时间顺序查看到。

```dbgcmd
0:002> !ttdext.tt 200:0
Setting position: 200:0
(954.3ffc): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 200:0
eax=00000000 ebx=012da718 ecx=7775396c edx=00000000 esi=012e1848 edi=012e1a08
eip=7775396c esp=014cf9f8 ebp=014cfbfc iopl=0         nv up ei ng nz ac po cy
cs=0023  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00000293
ntdll!NtWaitForWorkViaWorkerFactory+0xc:
7775396c c21400          ret     14h
```

使用[~ （线程状态）](---thread-status-.md)命令来确认，我们现在放置于第三个线程，3ffc。

```dbgcmd
0:002> ~
   0  Id: 954.1c74 Suspend: 4096 Teb: 00fdb000 Unfrozen
   1  Id: 954.1750 Suspend: 4096 Teb: 00fea000 Unfrozen
.  2  Id: 954.3ffc Suspend: 4096 Teb: 00fde000 Unfrozen
   3  Id: 954.36b8 Suspend: 4096 Teb: 00fe1000 Unfrozen
   4  Id: 954.3bc4 Suspend: 4096 Teb: 00fe4000 Unfrozen
   5  Id: 954.392c Suspend: 4096 Teb: 00fed000 Unfrozen
   6  Id: 954.32b4 Suspend: 4096 Teb: 00ff0000 Unfrozen
   7  Id: 954.337c Suspend: 4096 Teb: 00ff3000 Unfrozen
```


> [!NOTE]
> *~ S #* ，其中 *#* 也是大量线程，则会切换到给定的线程，但它不会更改跟踪中的当前位置。  当 *！ tt*是用于时间旅行到另一个线程的位置，你 （和调试器） 从内存中读取的任何值将查找该位置。 切换的线程时 *~ s #* ，调试器不会更改当前的位置在内部，用于内存中的所有查询。 此方法主要工作，以便 *~ s #* 无需重置调试器的内部循环。


## <a name="time-travel-debugging-extension-commands"></a>调试扩展命令按时间顺序查看

有关的信息`!tt`，`!positions`并`!index`命令查看[时间旅行调试-扩展命令](time-travel-debugging-extension-commands.md)。

 
## <a name="see-also"></a>请参阅

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

[时间旅行调试-记录跟踪](time-travel-debugging-record.md)

[调试-使用跟踪文件按时间顺序查看](time-travel-debugging-trace-file-information.md)

[时间旅行调试-示例应用程序演练](time-travel-debugging-walkthrough.md)

---






