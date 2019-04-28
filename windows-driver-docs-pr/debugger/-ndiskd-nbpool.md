---
title: ndiskd.nbpool
description: Ndiskd.nbpool 扩展显示有关 NET_BUFFER (NB) 池的信息。
ms.assetid: 4FCD48B7-C469-4057-A279-20522B00E80B
keywords:
- ndiskd.nbpool Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbpool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fb374611ea34d06b6ddb1ebc1f411b4e8e424aaa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335934"
---
# <a name="ndiskdnbpool"></a>!ndiskd.nbpool


**！ Ndiskd.nbpool**扩展显示有关的信息[ **NET\_缓冲区**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-structure) (NB) 池。 如果不带任何参数运行此扩展 ！ ndiskd 将显示在系统中的所有已分配的 NB 池的列表。

```console
!ndiskd.nbpool [-handle <x>] [-allocations] [-find <str>] [-findva <x>] [-findpa <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NB 池的句柄。

<span id="_______-allocations______"></span><span id="_______-ALLOCATIONS______"></span> *-allocations*   
显示所有分配 NBs。

<span id="_______-find______"></span><span id="_______-FIND______"></span> *-find*   
筛选分配 NBs 使用调试器表达式的列表。

<span id="_______-findva______"></span><span id="_______-FINDVA______"></span> *-findva*   
查找 NBs 跨给定虚拟地址。

<span id="_______-findpa______"></span><span id="_______-FINDPA______"></span> *-findpa*   
查找 NBs 跨给定的物理地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

输入 **！ ndiskd.nbpool**命令不带任何参数，以查看所有已分配的 NB 池的列表。 在此示例中，查找具有 Nnbf 标记 Netio 服务分配的 NB 池。 其句柄是 ffffdf801308ca40。

```console
2: kd> !ndiskd.nbpool
    NB Pool            Tag                 Allocated by                         
    ffffdf8013963a40   UDNb                NETIO!NetioAllocateNetBufferMdlAndDataPool+3c
    ffffdf801396aa40   TSNb                NETIO!NetioAllocateNetBufferMdlAndDataPool+3c
    ffffdf801397d4c0   StBn                NETIO!StreamPoolsInit+90
    ffffdf801308ca40   Nnbf                NETIO!NetioInitializeNetBufferListLibrary+dd
    ffffdf80131cba40   NDnd                ndis!DriverEntry+615
```

单击 NB 池的句柄或输入 **！ ndiskd.nbpool-处理**命令来检查其详细信息。

```console
2: kd> !ndiskd.nbpool ffffdf801308ca40


NB POOL

    Ndis handle        ffffdf801308ca40
    Allocation tag     Nnbf
    Owner
    Allocated by       NETIO!NetioInitializeNetBufferListLibrary+dd

    Flags              [No flags set]
    Structure size     0n176
    Data size          0

    All allocated NBs
```

若要浏览此 NB 池中包含 NBs，单击底部的"所有已分配 NBs"链接。 或者，您还可以输入 **！ ndiskd.nbpool-处理的分配**命令。 下面的示例中所示，此 NB 池包含 1024 个以上 NBs 因此 ！ ndiskd 提前退出。 可以使用-force 选项，若要解决此限制并查看所有此 NB 池中 NBs。

```console
2: kd> !ndiskd.nbpool ffffdf801308ca40 -allocations


ALL ALLOCATED NBs

    NB                 Active?                                                  
    ffffdf8016ea4360   Allocated
    ffffdf801744df50   Allocated
    ffffdf8016932860   Allocated
    ffffdf8016e31500   Allocated
    ffffdf80174eade0   Allocated
    ffffdf8017daa900   Allocated
    ffffdf8017c8c680   Allocated
    ffffdf80166b23b0   Allocated
    ffffdf80164fea70   Allocated
    ffffdf8012845990   Allocated
    ffffdf8017d692d0   Allocated
    ffffdf8017cdc090   Allocated
    ffffdf8012771780   Allocated
    ffffdf80158a3550   Allocated
    ffffdf8012eef5c0   Allocated
    ffffdf80127719d0   Allocated
    ffffdf8015119570   Allocated
    ffffdf8012e18d40   Allocated
    ffffdf8017929b10   Allocated
    ffffdf8016d4e430   Allocated

...

    ffffdf8015ffbbd0   Allocated
    ffffdf8015ec1b10   Freed
    ffffdf80158e56d0   Allocated
    ffffdf8016272110   Freed
    ffffdf8015d8e030   Freed
    ffffdf8015d8e770   Freed
    ffffdf80158ddc30   Freed
    ffffdf801584acc0   Freed
    ffffdf8015846b40   Freed
    ffffdf8015a06c50   Freed
    ffffdf801480c300   Freed
    ffffdf8015e48f50   Freed
    ffffdf8015de64e0   Freed
    ffffdf8015ddff50   Freed
    [Maximum of 1024 items read; quitting early. Rerun with the '-force' option
    to bypass this limit.]
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**NET\_BUFFER**](https://msdn.microsoft.com/windows/hardware/drivers/network/net-buffer-structure)

 

 






