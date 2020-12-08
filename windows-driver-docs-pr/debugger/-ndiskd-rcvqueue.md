---
title: ndiskd.rcvqueue
description: Ndiskd. rcvqueue 命令显示有关接收队列的信息。
keywords:
- ndiskd rcvqueue Windows 调试
ms.date: 06/26/2020
topic_type:
- apiref
api_name:
- ndiskd.rcvqueue
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 68809acfc32b912ca053442da40400a0ac8aceeb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813333"
---
# <a name="ndiskdrcvqueue"></a>!ndiskd.rcvqueue

**！ Ndiskd. rcvqueue** 命令显示有关接收队列的信息。

```console
!ndiskd.rcvqueue -handle <x> [-filters] [-mem] [-verbose] [-rcvqueueverbosity <x>] 
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 接收队列的句柄。

<span id="_______-filters______"></span><span id="_______-FILTERS______"></span>*-筛选器*   
显示队列中的筛选器。

<span id="_______-mem______"></span><span id="_______-MEM______"></span>*-mem*   
显示共享内存分配。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span>*-verbose*   
显示其他详细信息。

<span id="_______-rcvqueueverbosity______"></span><span id="_______-RCVQUEUEVERBOSITY______"></span>*-rcvqueueverbosity*   
要显示的详细信息的级别。

## <a name="dll"></a>DLL

Ndiskd.dll

## <a name="examples"></a>示例

若要获取接收队列句柄，请首先输入不带参数的 [**！ ndiskd**](-ndiskd-netadapter.md) 命令，以查看网络适配器列表、驱动程序及其句柄。 在以下示例中，查找 Microsoft ISATAP 适配器 \# 2 的 get-netadapter 句柄 ffff8083e02ce1a0。

```console
3: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffff8083e2668970   ffff8083e02ce1a0    Microsoft ISATAP Adapter #2
    ffff8083e210fae0   ffff8083e0f501a0    Microsoft Kernel Debug Network Adapter
```

接下来，使用 net 适配器的句柄，使用 **！ ndiskd-rcvqueues** 命令获取此网络适配器及其句柄的接收队列列表。 在此示例中，只有一个接收队列 (了) 句柄为 ffff8083e3a3d3a0 的默认接收队列。

```console
3: kd> !ndiskd.netadapter ffff8083e02ce1a0 -rcvqueues


RECEIVE QUEUES

    QueueId            Queue Handle        Processor Affinity                   
    0 [Default]        ffff8083e3a3d3a0    0:0000000000000000 (group:mask)
                       Queue Name:         [Zero-length string]
                       VM Name:            [Zero-length string]
```

现在，你可以使用队列句柄来检查接收队列的详细信息，并提供 **！ ndiskd. rcvqueue** 命令。

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

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)
