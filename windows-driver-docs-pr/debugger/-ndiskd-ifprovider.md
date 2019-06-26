---
title: ndiskd.ifprovider
description: Ndiskd.ifprovider 扩展显示有关 NDIS 接口提供程序 (IfProvider) 的信息。
ms.assetid: 89C406E5-81D3-42AA-BA15-3D7C093BCD3C
keywords:
- ndiskd.ifprovider Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ifprovider
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1126d8cb14d51cb95fe9b7ad79b38525aca163e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365755"
---
# <a name="ndiskdifprovider"></a>!ndiskd.ifprovider


**！ Ndiskd.ifprovider**扩展显示有关的信息[NDIS 接口提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider)(IfProvider)。 如果不带任何参数运行此扩展 ！ ndiskd 将显示所有已注册的 NDIS 接口提供程序的列表。

```console
!ndiskd.ifprovider [-handle <x>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
IfProvider 的句柄。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.ifprovider**注册 IfProviders 不带任何参数，以获取所有的列表的扩展。

```console
1: kd> !ndiskd.ifprovider
    IfProvider                                                                  
    ffffd20d14334180 - wanarp
    ffffd20d1264a950 - wfplwfs
    ffffd20d11deae00 - The NDIS loopback provider
    ffffd20d11deae70 - The NDIS interface provider
```

您可以看到从上一示例的调试对象计算机具有注册的四个接口提供程序。 其中两个 NDIS 接口提供程序。

**请注意**  接口提供程序是一个通用的概念，并且不要求具有微型端口驱动程序。 虽然微型端口驱动程序可能会选择将注册为接口提供程序，如果需要，大多数微型端口驱动程序不这样做因为 NDIS 具有内置的接口提供程序。 NDIS 内置接口提供程序会自动提供用于每个微型端口驱动程序、 轻型筛选器 (LWF) 的每个模块和环回接口的接口。 有关详细信息，请参阅[NDIS 接口提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider)。

 

下面的示例演示了在上一示例中，其句柄是 ffffd20d14334180"wanarp"接口提供程序的详细信息。

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

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

[注册为接口提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/registering-as-an-interface-provider)

 

 






