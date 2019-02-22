---
title: ndiskd.netpacket
description: Ndiskd.netpacket 扩展显示 NET_PACKET 结构有关的信息。
ms.assetid: 304BA2CF-B6BC-452C-8543-9B872054AA9E
keywords:
- ndiskd.netpacket Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netpacket
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3a7605566839d3962e73a36aaf5689cae1d77dc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546359"
---
# <a name="ndiskdnetpacket"></a>!ndiskd.netpacket


**！ Ndiskd.netpacket**扩展显示有关的信息[NET\_数据包](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)结构。

有关网络适配器 WDF 类扩展 (NetAdapterCx) 的详细信息，请参阅[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)。

```console
!ndiskd.netpacket [-handle <x>] [-basic] [-layout] [-checksum] [-data] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 网络地址\_数据包。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
显示基本信息。

<span id="_______-layout______"></span><span id="_______-LAYOUT______"></span> *-layout*   
显示数据包协议布局。

<span id="_______-checksum______"></span><span id="_______-CHECKSUM______"></span> *-checksum*   
显示数据包校验和信息。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-data*   
转储的有效负载内存。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

**请注意**  请参阅[对象摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)若要查看关系图说明的 NET 关系\_数据包 NetAdapterCx 中的其他对象的对象。

 

获取一个句柄的 NET\_数据包，请执行以下步骤：

1.  运行[ **！ ndiskd.netadapter** ](-ndiskd-netadapter.md)扩展。
2.  单击已安装了 NetAdapterCx 驱动程序 NetAdapter 句柄。
3.  单击"更多信息"链接到的 NetAdapter 的 NETADAPTER 对象运行的权限[ **！ ndiskd.cxadapter** ](-ndiskd-cxadapter.md)扩展。
4.  输入 **！ ndiskd.cxadapter**命令*的数据路径*参数，以查看该 NETADAPTER 数据路径队列。
5.  单击其中一个数据路径队列句柄。
6.  单击该数据路径队列环形缓冲区的句柄。
7.  单击底部的环形缓冲区详细信息，以查看它包含的元素上"列出的所有元素"链接。

步骤 1-4 在此过程的详细信息，请参阅示例上 **！ ndiskd.cxadapter**主题。 有关此过程的步骤 5 的详细信息，请参阅 》 上的示例[ **！ ndiskd.netqueue** ](-ndiskd-netqueue.md)主题。 有关此过程的步骤 6-7 的详细信息，请参阅 》 上的示例[ **！ ndiskd.netrb** ](-ndiskd-netrb.md)主题。
在以下示例中，查找句柄的第一个 NET\_数据包，ffffd1022d000040。

```console
0: kd> !ndiskd.netrb ffffd1022d000000 -dump

    [000] ffffd1022d000040 - NET_PACKET
    [001] ffffd1022d0000c0 - NET_PACKET
    [002] ffffd1022d000140 - NET_PACKET
    [003] ffffd1022d0001c0 - NET_PACKET
    [004] ffffd1022d000240 - NET_PACKET
    [005] ffffd1022d0002c0 - NET_PACKET
    
    ...

    [07b] ffffd1022d003dc0 - NET_PACKET
    [07c] ffffd1022d003e40 - NET_PACKET
    [07d] ffffd1022d003ec0 - NET_PACKET
    [07e] ffffd1022d003f40 - NET_PACKET
    [07f] ffffd1022d003fc0 - NET_PACKET
```

通过单击句柄上的此 NET\_数据包或通过输入 **！ ndiskd.netpacket-处理**命令行中，可以查看此网络的详细信息\_数据包，其中包括包含它的环形缓冲区数据路径队列，其中包含其环形缓冲区和其第一个片段的句柄。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

现在可以使用任何其他组合的基本说明 **！ ndiskd.netpacket**参数或所有这些，若要查看此片段的特定信息。 以下示例使用所有参数。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040 -basic -layout -checksum -data

    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090


    Protocol Layout                                                             

    Layer 2 Type       ETHERNET
    Header Length      0n14

    Layer 3 Type       IPV4_NO_OPTIONS
    Header Length      0n20

    Layer 4 Type       UDP
    Header Length      8


    Checksum Information                                                        

    Layer 2            TX_PASSTHROUGH
    Layer 3            TX_REQUIRED
    Layer 4            TX_PASSTHROUGH


    Payload data                                                                

    Fragment           ffffd1022d000040
    ffffd102303e8332  00 00 01 02 71 68 0a 89-be 39 e0 00 00 16 94 04  ····qh···9······
    ffffd102303e8342  00 00 22 00 fa 01 00 00-00 01 03 00 00 00 e0 00  ··"·············
    ffffd102303e8352  00 fc   
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_数据包](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

 

 






