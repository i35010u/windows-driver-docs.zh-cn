---
title: ndiskd.netrb
description: Ndiskd.netrb 扩展显示 NET_RING 结构有关的信息。
ms.assetid: 2D749E7E-00A5-422B-B785-B8DB3393A74F
keywords:
- ndiskd.netrb Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.netrb
api_type:
- NA
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f8b9a6c2d7c62430a987c420df1ad026c8509b84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335936"
---
# <a name="ndiskdnetrb"></a>!ndiskd.netrb


**！ Ndiskd.netrb**扩展显示有关的信息[NET\_环\_缓冲区](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-ring-buffer)结构。

有关网络适配器 WDF 类扩展 (NetAdapterCx) 的详细信息，请参阅[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)。

```console
!ndiskd.netrb [-handle <x>] [-basic] [-dump] [-elementtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 网络地址\_环\_缓冲区。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span> *-basic*   
显示基本信息。

<span id="_______-dump______"></span><span id="_______-DUMP______"></span> *-dump*   
显示有关每个元素的信息在 NET\_环\_缓冲区。

<span id="_______-elementtype______"></span><span id="_______-ELEMENTTYPE______"></span> *-elementtype*   
要引用的环形缓冲区元素时使用的数据类型为字符串。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

**请注意**  请参阅[对象摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)若要查看关系图说明的 NET 关系\_环\_NetAdapterCx 中的其他对象使用的缓冲区对象。

 

获取一个句柄的 NET\_环\_缓冲区，请执行以下步骤：

1.  运行[ **！ ndiskd.netadapter** ](-ndiskd-netadapter.md)扩展。
2.  单击已安装了 NetAdapterCx 驱动程序 NetAdapter 句柄。
3.  单击"更多信息"链接到的 NetAdapter 的 NETADAPTER 对象运行的权限[ **！ ndiskd.cxadapter** ](-ndiskd-cxadapter.md)扩展。
4.  输入 **！ ndiskd.cxadapter**命令*的数据路径*参数，以查看该 NETADAPTER 数据路径队列。
5.  单击其中一个数据路径队列句柄。

步骤 1-4 在此过程的详细信息，请参阅示例上 **！ ndiskd.cxadapter**主题。 有关此过程的步骤 5 的详细信息，请参阅 》 上的示例[ **！ ndiskd.netqueue** ](-ndiskd-netqueue.md)主题。
在以下示例中，查找此 NETTXQUEUE 环形缓冲区、 ffffd1022d000000 的句柄。

```console
0: kd> !ndiskd.netqueue ffffd1022f512700

    NETTXQUEUE         00002efdd0aed9a8
    Ring buffer        ffffd1022d000000

    Switch to EC thread

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtQueueAdvance                        fffff80034152af8   RtEthSample+2af8
    EvtQueueArmNotification                fffff80034159a94   RtEthSample+9a94
    EvtQueueCancel                         fffff800341598d8   RtEthSample+98d8
```

通过单击环形缓冲区或通过输入的句柄 **！ ndiskd.netrb-处理**命令在命令行中，你可以看到此网络的详细信息\_环\_缓冲区，包括它包含的元素数量和其开始和结束索引的地址。

```console
0: kd> !ndiskd.netrb ffffd1022d000000

    NET_RING    ffffd1022d000000

    Number of elements 0x080
    Owned by OS        0x080
    Owned by Client    00000

    Begin Index        0x078 (ffffd1022d003c40 - NET_PACKET)
    Next Index         0x078 (ffffd1022d003c40 - NET_PACKET)
    End Index          0x078 (ffffd1022d003c40 - NET_PACKET)

    List all elements
```

若要查看此 NET\_环\_缓冲区的元素，单击"列出的所有元素"底部其详细信息的链接，或输入 **！ ndiskd.netrb-转储**命令在命令行上。 下面的示例有为简便起见 excised 中间元素。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx)](https://docs.microsoft.com/windows-hardware/drivers/netcx)

[对象的摘要](https://docs.microsoft.com/windows-hardware/drivers/netcx/summary-of-objects)

[NET\_RING\_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/netcx/net-ring-buffer)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

 

 






