---
title: ndiskd.filterdriver
description: Ndiskd.filterdriver 扩展显示有关 NDIS 筛选器驱动程序的信息。 如果不带任何参数运行此扩展，ndiskd 将显示所有筛选器驱动程序的列表。
ms.assetid: 9FE3E885-98BC-4FCC-9E1C-DBECD070F92A
keywords:
- ndiskd.filterdriver Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.filterdriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7d96bca08f92724ba08f59a32cdf4f93df98a170
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364313"
---
# <a name="ndiskdfilterdriver"></a>!ndiskd.filterdriver


**！ Ndiskd.filterdriver**扩展显示有关 NDIS 筛选器驱动程序的信息。 如果不带任何参数运行此扩展 ！ ndiskd 将显示所有筛选器驱动程序的列表。

```console
!ndiskd.filterdriver [-handle <x>] [-filters] [-handlers] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
NDIS 筛选器驱动程序的句柄。

<span id="_______-filters______"></span><span id="_______-FILTERS______"></span> *-filters*   
显示此驱动程序筛选器的实例。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span> *-handlers*   
显示此驱动程序筛选器处理程序。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.filterdriver**不带任何参数，以查看在系统上的所有筛选器驱动程序列表。 在下面的示例中，查找虚拟的 WiFi 筛选器驱动程序，其句柄是 ffffbc064cc83be0。

```console
0: kd> !ndiskd.filterdriver
    ffffbc064ccd4900 - QoS Packet Scheduler
    ffffbc064cc83be0 - Virtual WiFi Filter Driver
    ffffbc064cb91a10 - WFP vSwitch Layers LightWeight Filter
    ffffbc064cb8fd70 - WFP Native MAC Layer LightWeight Filter
    ffffbc064cb59b00 - WFP 802.3 MAC Layer LightWeight Filter
```

通过单击筛选器驱动程序处理上一示例中或通过使用它输入 **！ ndiskd.filterdriver-处理**命令在命令窗口中，你可以获取请参阅有关该筛选器驱动程序详细信息。 在这种情况下，例如，有此筛选器驱动程序的任何筛选器模块。

```console
0: kd> !ndiskd.filterdriver ffffbc064cc83be0


FILTER DRIVER

    Virtual WiFi Filter Driver

    Ndis handle        ffffbc064cc83be0
    Driver context     ffffbc064cc8e9d0
    Ndis API version   v6.50
    Driver version     v1.0
    Driver object      ffffbc064cc8e9d0
    Driver image       vwififlt.sys

    Bind flags         Optional, Modifying
    Class              [Zero-length string]
    References         1


FILTER MODULES

    Filter module                                                               
    [No filter modules were found]


HANDLERS

    Filter handler                         Function pointer   Symbol (if available)
    SetOptionsHandler                      [None]
    SetFilterModuleOptionsHandler          [None]
    AttachHandler                          fffff80787d83b60  bp
    DetachHandler                          fffff80787d84800  bp
    RestartHandler                         fffff80787d86e20  bp
    PauseHandler                           fffff80787d863e0  bp
    SendNetBufferListsHandler              fffff80787d814d0  bp
    SendNetBufferListsCompleteHandler      fffff80787d81940  bp
    CancelSendNetBufferListsHandler        fffff80787d842f0  bp
    ReceiveNetBufferListsHandler           fffff80787d817e0  bp
    ReturnNetBufferListsHandler            fffff80787d81a80  bp
    OidRequestHandler                      fffff80787d85ae0  bp
    OidRequestCompleteHandler              fffff80787d85fd0  bp
    DirectOidRequestHandler                fffff80787d84af0  bp
    DirectOidRequestCompleteHandler        fffff80787d84e80  bp
    CancelDirectOidRequestHandler          fffff80787d841d0  bp
    DevicePnPEventNotifyHandler            fffff80787d849e0  bp
    NetPnPEventHandler                     fffff80787d85a40  bp
    StatusHandler                          fffff80787d877c0  bp
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

 

 






