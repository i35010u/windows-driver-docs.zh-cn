---
title: lpc
description: Lpc 扩展显示在目标系统中的所有本地过程调用 (LPC) 端口和消息有关的信息。
ms.assetid: d474aeca-fb12-424a-b57e-360215d0305c
keywords:
- LPC （本地/轻型过程调用）
- lpc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lpc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3e7d92d68ccd103c89f747baf87557e837778c39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546638"
---
# <a name="lpc"></a>!lpc


**重要**   Lpc 现在在 alpc 中模拟，请使用 ！ alpc 扩展相反。

 
**！ Lpc**扩展目标系统中显示的所有本地过程调用 (LPC) 端口和消息有关的信息。

```dbgcmd
!lpc message MessageID 
!lpc port Port 
!lpc scan Port 
!lpc thread Thread 
!lpc PoolSearch 
!lpc
```

## <a name="span-idddklpcdbgspanspan-idddklpcdbgspanparameters"></a><span id="ddk__lpc_dbg"></span><span id="DDK__LPC_DBG"></span>参数


<span id="_______message______"></span><span id="_______MESSAGE______"></span> **message**   
（Windows Server 2003、 Windows XP 和 Windows 2000 仅）显示一条消息，例如，如果有包含队列和等待此消息的线程中的消息的服务器端口有关的信息。

<span id="_______MessageID______"></span><span id="_______messageid______"></span><span id="_______MESSAGEID______"></span> *MessageID*   
（Windows Server 2003、 Windows XP 和 Windows 2000 仅）指定要显示的消息的消息 ID。 如果此参数的值为 0 或省略此参数，则 **！ lpc 消息**命令显示消息的摘要列表。 （在 Windows 2000 Service Pack 1 (SP1) 中，该摘要包括 LPC 区域中的所有消息。 在 Windows 2000 Service Pack 2 (SP2)、 Windows XP 和更高版本的 Windows 中，该摘要包括中的内核池的所有消息。 Paged-out 消息不包含。)

<span id="_______port______"></span><span id="_______PORT______"></span> **port**   
（Windows Server 2003、 Windows XP 和 Windows 2000 仅）显示端口信息，例如端口、 其信号量状态、 其队列中的消息、 其断开队列、 其句柄计数、 引用和相关的端口中的线程的名称。

<span id="_______scan______"></span><span id="_______SCAN______"></span> **scan**   
（Windows Server 2003、 Windows XP 和 Windows 2000 仅）显示有关指定的端口以及连接到它的所有端口的摘要信息。

<span id="_______Port______"></span><span id="_______port______"></span><span id="_______PORT______"></span> *端口*   
（Windows Server 2003、 Windows XP 和 Windows 2000 仅）指定要显示的端口的十六进制地址。 如果 **！ lpc 端口**使用命令，并*端口*为 0 或省略，将显示所有 LPC 端口的摘要列表。 如果 **！ lpc 扫描**使用命令时，*端口*必须指定实际端口的地址。

<span id="_______thread______"></span><span id="_______THREAD______"></span> **thread**   
（Windows Server 2003、 Windows XP 和 Windows 2000 仅）显示包含其断开端口队列中的指定的线程的所有端口的端口信息。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *线程*   
（Windows Server 2003、 Windows XP 和 Windows 2000 仅）指定线程的十六进制的地址。 如果这是 0 或被省略， **！ lpc 线程**命令显示所有线程执行的任何 LPC 操作的摘要列表。

<span id="_______PoolSearch______"></span><span id="_______poolsearch______"></span><span id="_______POOLSEARCH______"></span> **PoolSearch**   
（Windows Server 2003 和 Windows XP 仅）确定是否 **！ lpc 消息**命令中搜索在内核池的消息。 每次 **！ lpc PoolSearch**是使用，此设置切换打开或关闭 （初始设置是不搜索内核池）。 这只会影响 **！ lpc 消息**指定一个非零值的命令*MessageID*。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p>
<p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

Lpc 有关的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

在 Windows Vista 和更高版本的 Windows 中不支持此扩展。

在 Windows Server 2003、 Windows XP 和 Windows 2000 中，使用 **！ lpc**不带任何参数的调试器命令窗口中显示此扩展的帮助。

如果必须标记为等待答复消息的线程，使用 **！ lpc 消息**命令和延迟消息的 ID。 此命令显示指定的消息，包含它的端口和所有相关的线程。

如果找不到消息，并且那里不读取错误 （例如"无法访问区域段"），服务器将收到该消息。

在这种情况下，服务器端口通常都可以通过使用找到 **！ lpc 线程**命令。 等待回复的线程会链接到服务器通信队列。 此命令将显示包含指定的线程的所有端口。 您知道端口地址后，使用 **！ lpc 端口**命令。 然后可以通过使用获取有关每个线程的更多特定信息 **！ lpc 线程**命令和每个线程的地址。

下面是来自此扩展从 Windows XP 系统输出的几个示例：

在此示例中，将显示所有端口 LPC 端口。

```dbgcmd
kd> !lpc port
Scanning 225 objects
       1  Port: 0xe1405650 Connection: 0xe1405650  Communication: 0x00000000  'SeRmCommandPort' 
       1  Port: 0xe141ef50 Connection: 0xe141ef50  Communication: 0x00000000  'SmApiPort' 
       1  Port: 0xe13c5740 Connection: 0xe13c5740  Communication: 0x00000000  'ApiPort' 
       1  Port: 0xe13d9550 Connection: 0xe13d9550  Communication: 0x00000000  'SbApiPort' 
       3  Port: 0xe13d8830 Connection: 0xe141ef50  Communication: 0xe13d8910  ' 
80000004  Port: 0xe13d8910 Connection: 0xe141ef50  Communication: 0xe13d8830  ' 
       3  Port: 0xe13d8750 Connection: 0xe13d9550  Communication: 0xe13a4030  ' 
       .....
```

在上一示例中，在地址 e14ae238 端口有任何消息;也就是说，所有消息均已都选取并没有新消息已到达。

```dbgcmd
kd> !lpc port e14ae238

Server connection port e14ae238  Name: ApiPort
 Handles: 1   References: 107
    Server process  : 84aa0140 (csrss.exe)
    Queue semaphore : 84a96da8
 Semaphore state 0 (0x0)
    The message queue is empty
    The LpcDataInfoChainHead queue is empty
```

在上一示例中，在 0xe14ae238 端口都具有已排入队列，但尚未由服务器提取的消息。

```dbgcmd
kd> !lpc port 0xe14ae238

Server connection port e14ae238  Name: ApiPort
 Handles: 1   References: 108
    Server process  : 84aa0140 (csrss.exe)
    Queue semaphore : 84a96da8
 Semaphore state 0 (0x0)
        Messages in queue:
 0000 e20d9b80 - Busy  Id=0002249c  From: 0584.0680  Context=00000021  [e14ae248 . e14ae248]
 Length=0098007c  Type=00000001 (LPC_REQUEST)
                   Data: 00000000 0002021e 00000584 00000680 002f0001 00000007
    The message queue contains 1 messages
    The LpcDataInfoChainHead queue is empty
```

其余的 Windows XP 示例与其他可用于此扩展的选项。

```dbgcmd
kd> !lpc message 222be
Searching message 222be in threads ...
Client thread 842a4db0 waiting a reply from 222be
Searching thread 842a4db0 in port rundown queues ...

Server communication port 0xe114a3c0
    Handles: 1   References: 1
    The LpcDataInfoChainHead queue is empty
        Connected port: 0xe1e7b948      Server connection port: 0xe14ae238

Client communication port 0xe1e7b948
    Handles: 1   References: 3
    The LpcDataInfoChainHead queue is empty

Server connection port e14ae238  Name: ApiPort
 Handles: 1   References: 107
    Server process  : 84aa0140 (csrss.exe)
    Queue semaphore : 84a96da8
 Semaphore state 0 (0x0)
    The message queue is empty
    The LpcDataInfoChainHead queue is empty
Done.
```

```dbgcmd
kd> !lpc thread 842a4db0
Searching thread 842a4db0 in port rundown queues ...

Server communication port 0xe114a3c0
    Handles: 1   References: 1
    The LpcDataInfoChainHead queue is empty
        Connected port: 0xe1e7b948      Server connection port: 0xe14ae238

Client communication port 0xe1e7b948
    Handles: 1   References: 3
    The LpcDataInfoChainHead queue is empty

Server connection port e14ae238  Name: ApiPort
 Handles: 1   References: 107
    Server process  : 84aa0140 (csrss.exe)
    Queue semaphore : 84a96da8
 Semaphore state 0 (0x0)
    The message queue is empty
    The LpcDataInfoChainHead queue is empty
```

```dbgcmd
kd> !lpc scan e13d8830
Scanning 225 objects
       3  Port: 0xe13d8830 Connection: 0xe141ef50  Communication: 0xe13d8910  ' 
80000004  Port: 0xe13d8910 Connection: 0xe141ef50  Communication: 0xe13d8830  ' 
Scanning 3 objects
```

 

 





