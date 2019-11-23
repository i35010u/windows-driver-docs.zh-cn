---
title: ndiskd.netpacket
description: Ndiskd. netpacket 扩展显示 NET_PACKET 结构的相关信息。
ms.assetid: 304BA2CF-B6BC-452C-8543-9B872054AA9E
keywords:
- ndiskd netpacket Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netpacket
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 71fc05678795a53d991d85a749ad4fc1d6dc7dff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837576"
---
# <a name="ndiskdnetpacket"></a>!ndiskd.netpacket


**！ Ndiskd netpacket**扩展显示有关[网络\_数据包](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)结构的信息。

有关网络适配器 WDF 类扩展（NetAdapterCx）的详细信息，请参阅[网络适配器 Wdf 类扩展（Cx）](https://docs.microsoft.com/windows-hardware/drivers/netcx)。

```console
!ndiskd.netpacket [-handle <x>] [-basic] [-layout] [-checksum] [-data] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 网络\_数据包的地址。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-基本*   
显示基本信息。

<span id="_______-layout______"></span><span id="_______-LAYOUT______"></span> *-布局*   
显示数据包协议布局。

<span id="_______-checksum______"></span><span id="_______-CHECKSUM______"></span> *-checksum*   
显示数据包校验和信息。

<span id="_______-data______"></span><span id="_______-DATA______"></span> *-数据*   
转储负载内存。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="examples"></a>示例
--------

**注意**  查看[对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)，以查看说明网络\_数据包对象与 NetAdapterCx 中其他对象的关系的关系图。

 

若要获取 NET\_数据包的句柄，请执行以下步骤：

1.  运行[ **！ ndiskd. get-netadapter**](-ndiskd-netadapter.md)扩展。
2.  单击安装了 NetAdapterCx 驱动程序的 Get-netadapter 的句柄。
3.  单击 Get-netadapter 的 GET-NETADAPTER 对象右侧的 "详细信息" 链接，以运行[ **！ ndiskd. cxadapter**](-ndiskd-cxadapter.md)扩展。
4.  输入包含 *-数据路径*参数的 **！ cxadapter**命令，以查看 get-netadapter 的数据路径队列。
5.  单击其中一个数据路径队列的句柄。
6.  单击该数据路径队列的环形缓冲区的句柄。
7.  单击环形缓冲区详细信息底部的 "列出所有元素" 链接，查看其包含的元素。

有关此过程中步骤1-4 的详细信息，请参阅 **！ ndiskd. cxadapter**主题中的示例。 有关此过程的步骤5的详细信息，请参阅《 [ **！ ndiskd. netqueue**](-ndiskd-netqueue.md)主题中的示例。 有关此过程中步骤6-7 的详细信息，请参阅[ **！ ndiskd. netrb**](-ndiskd-netrb.md)主题中的示例。
在下面的示例中，查找第一个网络\_PACKET，ffffd1022d000040 的句柄。

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

通过单击此 NET\_数据包的句柄，或在命令行上输入 **！ ndiskd** ，可以查看此网络\_数据包的详细信息，包括包含它的环形缓冲区、包含其环形缓冲区的数据路径队列，以及其第一个片段的句柄。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

你现在可以将基本说明与任何其他 **！ netpacket**参数或所有参数组合在一起，以查看此片段的特定信息。 下面的示例使用所有参数。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展（Ndiskd）** ](ndis-extensions--ndiskd-dll-.md)

[ **！ ndiskd。帮助**](-ndiskd-help.md)

[网络适配器 WDF 类扩展（Cx）](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[对象摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_数据包](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)

[ **！ ndiskd. get-netadapter**](-ndiskd-netadapter.md)

[ **!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[ **!ndiskd.netqueue**](-ndiskd-netqueue.md)

[ **!ndiskd.netrb**](-ndiskd-netrb.md)

 

 






