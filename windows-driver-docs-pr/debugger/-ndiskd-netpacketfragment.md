---
title: ndiskd.netpacketfragment
description: Ndiskd.netpacketfragment 扩展显示 NET_PACKET_FRAGMENT 结构有关的信息。
ms.assetid: 2075D682-45F5-414D-A8ED-0494B3550C77
keywords:
- ndiskd.netpacketfragment Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netpacketfragment
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 69314033a2e25162e1bed68545b05649f5545222
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363123"
---
# <a name="ndiskdnetpacketfragment"></a>!ndiskd.netpacketfragment


**！ Ndiskd.netpacketfragment**扩展显示有关的信息[NET\_数据包\_片段](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet-fragment)结构。

有关网络适配器 WDF 类扩展 (NetAdapterCx) 的详细信息，请参阅[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)。

```console
!ndiskd.netpacketfragment [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 网络地址\_数据包\_片段。

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
8.  单击其中一个[NET\_数据包](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)环形缓冲区的元素的列表中的对象。

步骤 1-4 在此过程的详细信息，请参阅示例上 **！ ndiskd.cxadapter**主题。 有关此过程的步骤 5 的详细信息，请参阅 》 上的示例[ **！ ndiskd.netqueue** ](-ndiskd-netqueue.md)主题。 有关此过程的步骤 6-7 的详细信息，请参阅 》 上的示例[ **！ ndiskd.netrb** ](-ndiskd-netrb.md)主题。 有关此过程的第 8 步的详细信息，请参阅 》 上的示例[ **！ ndiskd.netpacket** ](-ndiskd-netpacket.md)主题。
在以下示例中，查找此 NET 的第一个片段的句柄\_数据包，ffffd1022d000040。

```console
0: kd> !ndiskd.netpacket ffffd1022d000040


    NET_PACKET         ffffd1022d000040    Ring Buffer        ffffd1022d000000
    First fragment     ffffd1022d000040    NETTXQUEUE         ffffd1022f512700

    Client Context     ffffd1022d000090

    Show protocol layout
    Show checksum information
    Dump data payload
```

通过单击第一个片段的句柄或输入 **！ ndiskd.netpacketfragment-处理**命令在命令行中，你可以看到此网络的详细信息\_数据包\_片段，包括其虚拟地址，容量，以及它是否是在网络中的最后一个数据包\_数据包链的片段。

```console
0: kd> !ndiskd.netpacketfragment ffffd1022d000040

    NET_PACKET_FRAGMENT ffffd1022d000040

    Virtual Address    ffffd102303e82f8
    Capacity           0n92
    Valid Length       0n34
    Offset             0n58

    Last packet of chain
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_数据包\_片段](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet-fragment)

[NET\_数据包](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-packet)

[ **!ndiskd.netadapter**](-ndiskd-netadapter.md)

[ **!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[ **!ndiskd.netqueue**](-ndiskd-netqueue.md)

[ **!ndiskd.netrb**](-ndiskd-netrb.md)

[ **!ndiskd.netpacket**](-ndiskd-netpacket.md)

 

 






