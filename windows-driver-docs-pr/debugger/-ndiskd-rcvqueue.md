---
title: ndiskd.rcvqueue
description: Ndiskd.rcvqueue 命令显示有关接收队列的信息。
ms.assetid: 776A459F-A698-4BF6-8DAD-BEB15858AD7F
keywords:
- ndiskd.rcvqueue Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.rcvqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0fb090428027fd74f4774978bbc58bff6bf76029
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335912"
---
# <a name="ndiskdrcvqueue"></a>!ndiskd.rcvqueue


**！ Ndiskd.rcvqueue**命令显示有关接收队列的信息。

```console
!ndiskd.rcvqueue [-handle <x>] [-filters] [-mem] [-verbose] [-rcvqueueverbosity <x>] 
```

## <a name="span-idddkdevobjdbgspanspan-idddkdevobjdbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
必需。 接收队列句柄。

<span id="_______-filters______"></span><span id="_______-FILTERS______"></span> *-filters*   
队列显示筛选器。

<span id="_______-mem______"></span><span id="_______-MEM______"></span> *-mem*   
显示共享内存分配。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span> *-verbose*   
显示更多详细信息。

<span id="_______-rcvqueueverbosity______"></span><span id="_______-RCVQUEUEVERBOSITY______"></span> *-rcvqueueverbosity*   
要显示的详细信息级别。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Ndiskd.dll

<a name="examples"></a>示例
--------

若要获取接收队列句柄，首次进入[ **！ ndiskd.netadapter** ](-ndiskd-netadapter.md)命令不带任何参数，以查看网络适配器、 其驱动程序和其句柄的列表。 在以下示例中，查找 Microsoft ISATAP 适配器\#2 的 NetAdapter 句柄，ffff8083e02ce1a0。

```console
3: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffff8083e2668970   ffff8083e02ce1a0    Microsoft ISATAP Adapter #2
    ffff8083e210fae0   ffff8083e0f501a0    Microsoft Kernel Debug Network Adapter
```

接下来，使用网络适配器的句柄，使用 **！ ndiskd.netadapter-处理-rcvqueues**命令来获取其句柄以及此网络适配器的接收队列的列表。 在此示例中，还有一个仅接收与 ffff8083e3a3d3a0 句柄的队列 （默认）。

```console
3: kd> !ndiskd.netadapter ffff8083e02ce1a0 -rcvqueues


RECEIVE QUEUES

    QueueId            Queue Handle        Processor Affinity                   
    0 [Default]        ffff8083e3a3d3a0    0:0000000000000000 (group:mask)
                       Queue Name:         [Zero-length string]
                       VM Name:            [Zero-length string]
```

现在，可以使用队列句柄来检查接收队列的详细信息， **！ ndiskd.rcvqueue**命令。

```console
3: kd> !ndiskd.rcvqueue ffff8083e3a3d3a0


RECEIVE QUEUE

    [Zero-length string]

    VM name            [Zero-length string]
    QueueId            0
    Ndis handle        ffff8083e3a3d3a0

    Miniport           ffff8083e02ce1a0 - Microsoft ISATAP Adapter #2
    Open               [No associated Open]

    Type               Unspecified
    Flags              [No flags set]
    Allocated          Yes
    References         1

    Num filters        0
    Num buffers hint   0
    MSI-X entry        0
    Lookahead size     0
    Processor affinity 0:0000000000000000 (group:mask)

    Receive filter list
    Shared memory allocations
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

 

 






