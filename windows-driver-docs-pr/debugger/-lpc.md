---
title: lpc
description: Lpc 扩展显示有关目标系统中的所有本地过程调用 (LPC) 端口和消息的信息。
keywords:
- 'LPC (本地/轻型过程调用) '
- lpc Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- lpc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 22e9a563da7b4631976fc14f99246cff2c18280d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829989"
---
# <a name="lpc"></a>!lpc


**重要说明**  
Lpc 现在已在 alpc 中模拟，请改用！ alpc 扩展。

 
**！ Lpc** 扩展显示有关目标系统中的所有本地过程调用 (lpc) 端口和消息的信息。

```dbgcmd
!lpc message MessageID 
!lpc port Port 
!lpc scan Port 
!lpc thread Thread 
!lpc PoolSearch 
!lpc
```

## <a name="span-idddk__lpc_dbgspanspan-idddk__lpc_dbgspanparameters"></a><span id="ddk__lpc_dbg"></span><span id="DDK__LPC_DBG"></span>参数


<span id="_______message______"></span><span id="_______MESSAGE______"></span>**消息**   
 (Windows Server 2003、Windows XP 和 Windows 2000 仅) 显示消息的相关信息，例如包含队列中的消息的服务器端口和等待此消息的线程（如果有）。

<span id="_______MessageID______"></span><span id="_______messageid______"></span><span id="_______MESSAGEID______"></span>*MessageID*   
 (Windows Server 2003、Windows XP 和 Windows 2000 仅) 指定要显示的消息的消息 ID。 如果此参数的值为0或省略此参数，则 **！！消息** 命令显示消息的摘要列表。  (在带有 Service Pack 1 (SP1) 的 Windows 2000 中，摘要包含 LPC 区域中的所有消息。 在 Windows 2000 Service Pack 2 (SP2) 、Windows XP 和更高版本的 Windows 中，摘要包含内核池中的所有消息。 不包括分页的消息。 ) 

<span id="_______port______"></span><span id="_______PORT______"></span>**端口**   
 (Windows Server 2003、Windows XP 和 Windows 2000 仅) 显示端口信息，例如端口的名称、其信号量状态、队列中的消息、断开队列中的线程、其句柄计数、引用以及相关端口。

<span id="_______scan______"></span><span id="_______SCAN______"></span>**扫描**   
 (Windows Server 2003、Windows XP 和 Windows 2000 仅) 显示有关指定端口以及连接到该端口的所有端口的摘要信息。

<span id="_______Port______"></span><span id="_______port______"></span><span id="_______PORT______"></span>*端口*   
 (Windows Server 2003、Windows XP 和 Windows 2000 仅) 指定要显示的端口的十六进制地址。 如果使用了 **！ lpc 端口** 命令，并且 *端口* 为0或被省略，则显示所有 lpc 端口的摘要列表。 如果使用了 **！ lpc 扫描** 命令， *端口* 必须指定实际端口的地址。

<span id="_______thread______"></span><span id="_______THREAD______"></span>**thread**   
 (Windows Server 2003、Windows XP 和 Windows 2000 仅) 显示其断开端口队列中包含指定线程的所有端口的端口信息。

<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span>*Thread*   
 (Windows Server 2003、Windows XP 和 Windows 2000 仅) 指定线程的十六进制地址。 如果此为0或省略，则 **！ lpc thread** 命令显示执行任何 lpc 操作的所有线程的摘要列表。

<span id="_______PoolSearch______"></span><span id="_______poolsearch______"></span><span id="_______POOLSEARCH______"></span>**PoolSearch**   
 (Windows Server 2003 和 Windows XP 仅) 确定 **！ lpc 消息** 命令是否搜索内核池中的消息。 每次使用 **！ Lpc PoolSearch** 时，此设置将在初始设置)  (打开或关闭。 这只会影响为 *MessageID* 指定非零值的 **lpc 消息** 命令。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 LPCs 的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

Windows Vista 和更高版本的 Windows 不支持此扩展。

在 Windows Server 2003、Windows XP 和 Windows 2000 中，使用不带参数的 **！ lpc** 会在调试器命令窗口中显示此扩展的帮助。

如果有一个标记为 "等待对消息的答复" 的线程，请使用带有延迟消息 ID 的 **！ lpc message** 命令。 此命令显示指定的消息、包含该消息的端口以及所有相关线程。

如果找不到该消息，并且没有读取错误 (如 "无法访问区域段" ) ，则服务器接收到该消息。

在这种情况下，通常可以使用 **！ lpc thread** 命令查找服务器端口。 正在等待响应的线程将链接到服务器通信队列。 此命令将显示包含指定线程的所有端口。 了解端口地址后，请使用 **！ lpc 端口** 命令。 然后，可以通过将 **！ lpc thread** 命令与每个线程的地址一起使用来获取有关每个线程的更具体的信息。

下面是来自 Windows XP 系统的此扩展的输出的几个示例：

在此示例中，显示了所有端口 LPC 端口。

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

在上面的示例中，地址 e14ae238 处的端口没有消息;也就是说，已拾取所有消息，但没有收到新消息。

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

在上面的示例中，0xe14ae238 的端口包含已排队但尚未由服务器提取的消息。

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

其余 Windows XP 示例涉及可与此扩展一起使用的其他选项。

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

 

 





