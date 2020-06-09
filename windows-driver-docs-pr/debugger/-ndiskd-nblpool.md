---
title: ndiskd.nblpool
description: Ndiskd. nblpool 扩展显示 NET_BUFFER_LIST （NBL）池的相关信息。 如果运行不带任何参数的此扩展，则 ndiskd 会在系统中显示所有已分配的 NBL 池的列表。
ms.assetid: 78F8E45C-D13D-4628-A387-529291B4C50C
keywords:
- ndiskd nblpool Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nblpool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6942e19db80e3866a184c1a4a7e0ecdcda4eeee9
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534730"
---
# <a name="ndiskdnblpool"></a>!ndiskd.nblpool


**！ Ndiskd nblpool**扩展显示有关[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)（NBL）池的信息。 如果运行不带参数的此扩展，！ ndiskd 将显示系统中已分配的所有 NBL 池的列表。

```console
!ndiskd.nblpool [-handle <x>] [-basic] [-allocations] [-find <str>] [-findnb <str>] 
    [-findctx <str>] [-findctxtype <str>] [-findva <x>] [-findpa <x>]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NBL 池的句柄。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
显示有关 NBL 池的基本信息。

<span id="_______-allocations______"></span><span id="_______-ALLOCATIONS______"></span>*-分配*   
显示所有已分配的 Nbl。

<span id="_______-find______"></span><span id="_______-FIND______"></span>*-查找*   
使用调试器表达式筛选分配的 Nbl 的列表。

<span id="_______-findnb______"></span><span id="_______-FINDNB______"></span>*-findnb*   
按链接的[**网络 \_ 缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)秒（NBs）筛选已分配的 nbl 的列表。

<span id="_______-findctx______"></span><span id="_______-FINDCTX______"></span>*-findctx*   
按上下文区域筛选分配的 Nbl 的列表。

<span id="_______-findctxtype______"></span><span id="_______-FINDCTXTYPE______"></span>*-findctxtype*   
重写上下文区域的数据类型。

<span id="_______-findva______"></span><span id="_______-FINDVA______"></span>*-findva*   
查找 Nbl，其中包含跨越给定虚拟地址的 NB。

<span id="_______-findpa______"></span><span id="_______-FINDPA______"></span>*-findpa*   
查找 Nbl，其中包含跨越给定物理地址的 NB。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="examples"></a>示例
--------

输入不带参数的 **！ ndiskd**命令，以查看所有已分配的 NBL 池的列表。 在此示例中，使用 KDNr 标记查找由内核调试器网络接口卡（kdnic）分配的 NBL 池。 它的句柄为 ffffdf80147e4a40。

```console
2: kd> !ndiskd.nblpool
    NBL Pool           Tag                 Allocated by                         
    ffffdf80179b6a40   NiBP                WdNisDrv!CWFPLayer::Initialize+c6
    ffffdf8015ac6a40   EUNP                tunnel!TunnelEtherUdpGlobalInit+81
    ffffdf8015a78040   Nuio                ndisuio!ndisuioCreateBinding+15f
    ffffdf8015a77800   Nuio                ndisuio!ndisuioCreateBinding+13c
    ffffdf8015a63040   BaNB                rspndr!TopStartNetBufferModule+6d
    ffffdf8015a68a40   LLnb                mslldp!lldpProtSetOptions+49
    ffffdf8014654040   BaNB                lltdio!TopStartNetBufferModule+6d
    ffffdf801494ca40   Pcsb                pacer!PcFilterAttach+142
    ffffdf80147e4a40   KDNr                kdnic!NICAllocAdapter+178
    ffffdf80131ce040   bnvW                wfplwfs!DriverEntry+7a0
    ffffdf80139ffa40   Wfdp                wfplwfs!WfpRioInitialize+a4
    ffffdf8012061200   UNbl                NETIO!NetioAllocateNetBufferListNetBufferMdlAndDataPool+49
    ffffdf8013968a40   TcDN                NETIO!NetioAllocateNetBufferListNetBufferMdlAndDataPool+49
    ffffdf8013969a40   TNbl                NETIO!NetioAllocateNetBufferListNetBufferMdlAndDataPool+49
    ffffdf801397c040   StBn                NETIO!StreamPoolsInit+c1
    ffffdf8013088040   Wfra                NETIO!WfpNblInfoLibraryInit+b8
    ffffdf8012067440   Nnnn                NETIO!NetioInitializeNetBufferListLibrary+13e
    ffffdf8012067a40   Nnbl                NETIO!NetioInitializeNetBufferListLibrary+112
    ffffdf80131caa40   NDrt                ndis!ndisInitializePeriodicReceives+22f
    ffffdf80131d5a40   NDnd                ndis!DriverEntry+5e9
```

单击 NBL 池的句柄，或输入 **！ ndiskd**命令来检查其详细信息。

```console
2: kd> !ndiskd.nblpool ffffdf80147e4a40


NBL POOL

    Ndis handle        ffffdf80147e4a40
    Allocation tag     KDNr
    Owner
    Allocated by       kdnic!NICAllocAdapter+178

    Flags              CONTAINS_NET_BUFFER
    Structure size     0n544
    Context size       0
    Data size          0

    All allocated NBLs
```

若要浏览包含在此 NBL 池中的 Nbl，请单击底部的 "所有已分配的 Nbl" 链接。 另外，还可以输入 **！ ndiskd-分配**命令。 如以下示例中所示，此 NBL 池包含1024个以上的 Nbl，因此！ ndiskd 会提前退出。 可以使用-force 选项来解决此限制，并查看此 NBL 池中的所有 Nbl。

```console
2: kd> !ndiskd.nblpool ffffdf80147e4a40 -allocations


ALL ALLOCATED NBLs

    NBL                Active?                                                  
    ffffdf8014951940   Allocated
    ffffdf8014951b90   Allocated
    ffffdf8014951de0   Allocated
    ffffdf8014951030   Allocated
    ffffdf80149524a0   Allocated
    ffffdf80149526f0   Allocated
    ffffdf8014952940   Allocated
    ffffdf8014952b90   Allocated
    ffffdf8014952de0   Allocated
    ffffdf8014952030   Allocated
    ffffdf80149534a0   Allocated
    ffffdf80149536f0   Allocated
    ffffdf8014953940   Allocated
    ffffdf8014953b90   Allocated
    ffffdf8014953de0   Allocated
    ffffdf8014953030   Allocated
    ffffdf80149544a0   Allocated
    ffffdf80149546f0   Allocated
    ffffdf8014954940   Allocated

...

    ffffdf80148b0b90   Allocated
    ffffdf80148b0de0   Allocated
    ffffdf80148b0030   Allocated
    ffffdf80148b14a0   Allocated
    ffffdf80148b16f0   Allocated
    ffffdf80148b1940   Allocated
    ffffdf80148b1b90   Allocated
    ffffdf80148b1de0   Allocated
    ffffdf80148b1030   Allocated
    [Maximum of 1024 items read; quitting early. Rerun with the '-force' option
    to bypass this limit.]
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**网络 \_ 缓冲区 \_ 列表**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-structure)

[**网络 \_ 缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-structure)

 

 






