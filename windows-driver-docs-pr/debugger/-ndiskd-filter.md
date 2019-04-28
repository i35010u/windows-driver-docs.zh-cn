---
title: ndiskd.filter
description: Ndiskd.filter 扩展显示有关 NDIS 轻型筛选器 （lwf） 转变的信息。 如果不带任何参数运行此扩展，ndiskd 将显示所有 LWFs 的列表。
ms.assetid: 4cf0f8bc-a15a-49db-b7db-13d60fd0c767
keywords:
- ndiskd.filter Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.filter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 294b53f8dc106c61712fc123b4b535a988d5ffab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335990"
---
# <a name="ndiskdfilter"></a>!ndiskd.filter


**！ Ndiskd.filter**扩展显示有关 NDIS 轻型筛选器 （lwf） 转变的信息。 如果不带任何参数运行此扩展 ！ ndiskd 将显示所有 LWFs 的列表。

```console
!ndiskd.filter [-handle <x>] [-findname <any>] [-handlers] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS 轻型筛选器的句柄。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span> *-findname*   
通过名称前缀来筛选 LWFs。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-handlers*   
显示此 LWF 筛选器处理程序。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

输入 **！ ndiskd.filter**命令不带任何参数，以获取所有筛选器的列表。 在此示例中，查找 ffff8083e14e8460 句柄。 请注意，此句柄是本身的筛选器和嵌套在其关联的筛选器下*驱动程序*，QoS 数据包计划程序。

```console
3: kd> !ndiskd.filter
ffff8083e1a7fd90 - QoS Packet Scheduler
  Filter ffff8083e14e8460, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
ffff8083e1a96b80 - Virtual WiFi Filter Driver
ffff8083e19c4b70 - WFP vSwitch Layers LightWeight Filter
ffff8083e19a6ad0 - WFP Native MAC Layer LightWeight Filter
  Filter ffff8083e43df8f0, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
ffff8083e19a6d70 - WFP 802.3 MAC Layer LightWeight Filter
  Filter ffff8083e0d89c70, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
```

通过使用此筛选器句柄，我们现在可以看到更多详细的信息，例如其状态、 更高版本的筛选器句柄和较低的筛选器句柄。

```console
3: kd> !ndiskd.filter ffff8083e14e8460


FILTER

    Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000

    Ndis handle        ffff8083e14e8460
    Filter driver      ffff8083e1a7fd90 - QoS Packet Scheduler
    Module context     ffff8083e26953e0
    Miniport           ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
    Network interface  ffff8083e200f010

    State              Running
    Datapath           Send only
    References         1
    Flags              RUNNING
    More flags         OID_TOP

    Higher filter      ffff8083e0d89c70 - Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000
    Lower filter       ffff8083e43df8f0 - Microsoft Kernel Debug Network Adapter-WFP Native MAC Layer LightWeight Filter-0000

    Driver handlers
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

 

 






