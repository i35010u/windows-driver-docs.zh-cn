---
title: ndiskd.ifprovider
description: Ndiskd. ifprovider 扩展显示有关 NDIS 接口提供程序（IfProvider）的信息。
ms.assetid: 89C406E5-81D3-42AA-BA15-3D7C093BCD3C
keywords:
- ndiskd ifprovider Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ifprovider
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 052e809ac9dcec973315345007eb2505a318fb20
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534930"
---
# <a name="ndiskdifprovider"></a>!ndiskd.ifprovider


**！ Ndiskd ifprovider**扩展显示有关[NDIS 接口提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider)（ifprovider）的信息。 如果运行不带参数的此扩展，！ ndiskd 将显示所有已注册 NDIS 接口提供程序的列表。

```console
!ndiskd.ifprovider [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
IfProvider 的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Ndiskd

<a name="examples"></a>示例
--------

运行不带参数的 **！ ndiskd ifprovider**扩展，以获取所有已注册 IfProviders 的列表。

```console
1: kd> !ndiskd.ifprovider
    IfProvider                                                                  
    ffffd20d14334180 - wanarp
    ffffd20d1264a950 - wfplwfs
    ffffd20d11deae00 - The NDIS loopback provider
    ffffd20d11deae70 - The NDIS interface provider
```

可以从前面的示例中看到，调试对象计算机注册了四个接口提供程序。 其中两个是 NDIS 接口提供程序。

**注意**   接口提供程序是一种通用概念，无需是小型端口驱动程序。 如果需要，微型端口驱动程序可以选择将注册为接口提供程序，大多数微型端口驱动程序不会这样做，因为 NDIS 具有内置接口提供程序。 NDIS 内置接口提供程序自动为每个微型端口驱动程序、每个轻型筛选器（LWF）模块和环回接口提供接口。 有关详细信息，请参阅[NDIS interface provider](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider)。

 

下面的示例显示了上一示例中 "wanarp" 接口提供程序的详细信息，其句柄为 ffffd20d14334180。

```console
1: kd> !ndiskd.ifprovider ffffd20d14334180


IF PROVIDER

    wanarp
    Ndis handle        ffffd20d14334180


INTERFACES

    Interface                                                                   
    [No interfaces found]


HANDLERS

    Protocol handler                       Function pointer   Symbol (if available)
    QueryObjectHandler                     fffff80d2f0414b0  bp wanarp!WanNdisIfQueryHandler
    SetObjectHandler                       fffff80d2f04bd10  bp wanarp!WanNdisIfSetHandler
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[注册为接口提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider)

 

 






