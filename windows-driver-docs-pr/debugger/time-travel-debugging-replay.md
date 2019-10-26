---
title: 时光穿越调试 - 重放跟踪
description: 本部分介绍如何重播时间行程跟踪。
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2639b5e4654a2e52554295243aa0ada484b8b1a3
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916140"
---
# <a name="time-travel-debugging---replay-a-trace"></a>时光穿越调试 - 重放跟踪

![显示时钟的小时间旅行徽标](images/ttd-time-travel-debugging-logo.png) 

本部分介绍如何重播时间行程跟踪，并在时间前后导航。

## <a name="command-time-travel-navigation"></a>命令时间旅行导航

使用尾随负号，并使用以下命令及时返回。

| 命令  | 
|----------------|
| p-（后退） | 
| t-（Trace Back）| 
| g-（返回）   |

有关详细信息，请参阅[行程调试-导航命令](time-travel-debugging-navigation-commands.md)。 

## <a name="ribbon-button-time-travel-navigation"></a>功能区按钮时间行程导航

或者，使用功能区按钮在跟踪中导航。

![显示 "开始记录" 复选框的 WinDbg 预览屏幕截图](images/ttd-ribbon-buttons.png)


## <a name="example-ttd-trace-replay"></a>示例 TTD 跟踪重播

使用 g-command 来向后执行，直到到达事件或 TTD 跟踪的开头。 可以停止向后执行的事件与停止执行的事件相同。 在此示例中，已达到跟踪的开头。


```dbgcmd
0:000> g-
TTD: Start of trace reached.
(3f78.4274): Break instruction exception - code 80000003 (first/second chance not available)
Time Travel Position: 29:0
ntdll!ZwTestAlert+0x14:
00007ffc`61f789d4 c3              ret
```

使用[p （Step）](https://docs.microsoft.com/windows-hardware/drivers/debugger/p--step-)命令在 TTD 跟踪中前进。 

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

你还可以使用[t （Trace）](https://docs.microsoft.com/windows-hardware/drivers/debugger/t--trace-)命令在跟踪中导航。

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


使用 p-command 在 TTD 跟踪中向后单步执行。 

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

你还可以使用 t-命令来及时向后导航。


## <a name="tt-navigation-commands"></a>！ tt 导航命令

使用！！命令向前或向后导航，方法是跳到跟踪中的给定位置。 

！ tt [position]

提供以下任意格式的时间位置以在该时间点旅行。
           
- 如果 [position] 为介于0到100之间的十进制数字，则它会在跟踪中接近该百分比。 例如 `!tt 50` 向跟踪的一半。

- 如果 {position} 为 #： #，其中 # 是十六进制数字，则将其移动到该位置。 例如，`!tt 1A0:12F` 传播到跟踪中的位置1A0：12F。

有关详细信息，请参阅[行程调试-！ tt （行程时间）](time-travel-debugging-extension-tt.md)。


## <a name="positions"></a>！位置

使用 `!positions` 显示所有活动线程，包括它们在跟踪中的位置。 有关详细信息，请参阅[行程调试-！位置（旅行时间）](time-travel-debugging-extension-positions.md)。

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
此示例显示当前位置有8个线程。 当前线程为3604，标记为 ">"。  

> [!TIP] 
> 显示当前线程及其位置列表的另一种方法是使用数据模型 dx 命令：
>
> `dx -g @$curprocess.Threads.Select(t => new { IsCurrent = t.Id == @$curthread.Id, ThreadId = t.Id, Position = t.TTD.Position })`
>

使用 user mode [~ （Thread Status）](---thread-status-.md)命令显示相同的八个线程，并使用 "." 标记当前线程：

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

单击 "！位置" 输出中第三个线程（3FFC）旁边的链接，以便在跟踪中的该位置到达此位置（200:0）。

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

使用[~ （Thread Status）](---thread-status-.md)命令确认我们目前定位于第三个线程3ffc。

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
> *~ S #* ，其中 *#* 是一个线程号，还切换到给定线程，但它不会更改跟踪中的当前位置。  当使用 *！ tt*来使到达另一个线程的位置时，将在该位置查找您（和调试器）从内存中读取的任何值。 当使用 *~ s #* 切换线程时，调试器不会内部更改当前位置，这用于所有内存查询。 这主要以这种方式运行，因此 *~ s #* 不必重置调试器的内部循环。


## <a name="time-travel-debugging-extension-commands"></a>行程调试扩展命令

有关 `!tt`的信息，[请参阅 `!positions` 和 `!index` 命令。](time-travel-debugging-extension-commands.md)

 
## <a name="see-also"></a>另请参阅

[行程调试-概述](time-travel-debugging-overview.md)

[旅行调试-记录跟踪](time-travel-debugging-record.md)

[时间行程调试-使用跟踪文件](time-travel-debugging-trace-file-information.md)

[旅行调试-示例应用演练](time-travel-debugging-walkthrough.md)

