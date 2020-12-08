---
title: ndiskd.nbpool
description: Ndiskd. nbpool 扩展显示 NET_BUFFER (NB) 池的相关信息。
keywords:
- ndiskd nbpool Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.nbpool
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e0732696d4b0e2535b780254664f3bd54edf8f5c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814065"
---
# <a name="ndiskdnbpool"></a>!ndiskd.nbpool


**！ Ndiskd nbpool** 扩展显示 (NB) 池的 [**网络 \_ 缓冲区**](../network/net-buffer-structure.md)的相关信息。 如果运行不带参数的此扩展，！ ndiskd 将显示系统中所有已分配的 NB 池的列表。

```console
!ndiskd.nbpool [-handle <x>] [-allocations] [-find <str>] [-findva <x>] [-findpa <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NB 池的句柄。

<span id="_______-allocations______"></span><span id="_______-ALLOCATIONS______"></span>*-分配*   
显示所有已分配的 NBs。

<span id="_______-find______"></span><span id="_______-FIND______"></span>*-查找*   
使用调试器表达式筛选分配的 NBs 的列表。

<span id="_______-findva______"></span><span id="_______-FINDVA______"></span>*-findva*   
查找跨给定虚拟地址的 NBs。

<span id="_______-findpa______"></span><span id="_______-FINDPA______"></span>*-findpa*   
查找跨给定物理地址的 NBs。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

输入不带参数的 **！ ndiskd** 命令，以查看所有已分配的 NB 池的列表。 在此示例中，查找 Netio 服务使用 Nnbf 标记分配的 NB 池。 它的句柄为 ffffdf801308ca40。

```console
2: kd> !ndiskd.nbpool
    NB Pool            Tag                 Allocated by                         
    ffffdf8013963a40   UDNb                NETIO!NetioAllocateNetBufferMdlAndDataPool+3c
    ffffdf801396aa40   TSNb                NETIO!NetioAllocateNetBufferMdlAndDataPool+3c
    ffffdf801397d4c0   StBn                NETIO!StreamPoolsInit+90
    ffffdf801308ca40   Nnbf                NETIO!NetioInitializeNetBufferListLibrary+dd
    ffffdf80131cba40   NDnd                ndis!DriverEntry+615
```

单击 NB 池的句柄，或输入 **！ ndiskd** 命令以检查其详细信息。

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

若要浏览此 NB 池中包含的 NBs，请单击底部的 "所有已分配的 NBs" 链接。 另外，还可以输入 **！ ndiskd-分配** 命令。 如以下示例中所示，此 NB 池包含1024多个 NBs，因此！ ndiskd 提前退出。 可以使用-force 选项来解决此限制，并查看此 NB 池中的所有 NBs。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**网络 \_ 缓冲区**](../network/net-buffer-structure.md)

 

