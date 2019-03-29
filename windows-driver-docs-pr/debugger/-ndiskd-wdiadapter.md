---
title: ndiskd.wdiadapter
description: Ndiskd.wdiadapter 扩展显示 WDIWiFi CAdapter 结构有关的信息。 如果不带任何参数运行此扩展，ndiskd 将显示所有 WDIWiFi CAdapter 结构的列表。
ms.assetid: 1AC069E8-CF87-459B-9C56-DDC1A6F765A8
keywords:
- ndiskd.wdiadapter Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.wdiadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 36d8b83793d4b8f09e7401084259ed498cb146c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562646"
---
# <a name="ndiskdwdiadapter"></a>!ndiskd.wdiadapter


**！ Ndiskd.wdiadapter**扩展显示有关 WDIWiFi 信息 ！CAdapter 结构。 如果不带任何参数运行此扩展 ！ ndiskd 将显示一组所有 WDIWiFi ！CAdapter 结构。

有关 WDI 微型端口驱动程序的详细信息，请参阅[WDI 微型端口驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/wdi-miniport-driver-design-guide)。

WDI 微型端口驱动程序引用的详细信息，请参阅[WDI 微型端口驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/dn926075)。

```console
!ndiskd.wdiadapter [-handle <x>] [-pm] [-rcvfilter] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
CAdapter 对象的句柄。

<span id="_______-pm______"></span><span id="_______-PM______"></span> *-pm*   
显示电源管理状态和功能。

<span id="_______-rcvfilter______"></span><span id="_______-RCVFILTER______"></span> *-rcvfilter*   
显示接收的筛选功能。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.wdiadapter**扩展不带任何参数，以查看所有 CAdapter 对象，以及为每个其 WDI 适配器的详细信息的列表。 在以下示例中，没有只有一个 CAdapter 结构。 其关联的 WDI 适配器的句柄是 ffffc804af396000。

```console
1: kd> !ndiskd.wdiadapter
    CAdapter                                                                    
    ffffc804af396000 - WDI Adapter


WDI ADAPTER

    Object             ffffc804af396000
    Miniport           ffffc804b9e6f1a0
    WDI driver         ffffc804b8ce7c40 - WDI MiniDriver
    NetGuid            47cb3aa5-e29c-4628-80bd-5023c53fcccb
    Power              D0

    CCtlPlane          ffffc804af396080
    CTxMgr             ffffc804af399790


DEVICE COMMANDS

    Scheduler state    DeviceCommandSchedulerStateInit
    [No queued device commands found]

Device Command Scheduler


SERIALIZED JOBS

    Job                State               Type               Child             
    ffffc804b9f33000   StepPending         WiFiJobMiniportInitialize



ACTIVE JOBS

    Job                State               Type               Child             
    ffffc804b9f33000   StepPending         WiFiJobMiniportInitialize



EVENTS

    Processing?        No

    Event              Status              Type                                 
    [No events found]

Event Queue


MORE INFORMATION

    Power management                       Receive filtering
```

现在，您可以在"电源管理"和"接收筛选"CAdapter 结构的说明，底部的链接上单击，也可以输入 **！ ndiskd.wdiadapter-处理**命令与 *-pm*或 *-rcvfilter*选项。 下面的示例显示了为输出 *-rcvfilter*选项。

```console
1: kd> !ndiskd.wdiadapter ffffc804af396000 -rcvfilter


RECEIVE FILTER

    Current Configuration

    Revision                               0
    Flags                                  0
    Enabled filter types                   [No flags set]
    Enabled queue types                    [No flags set]
    Max Queues                             0
    Queue properties                       [No flags set]
    Filter tests                           [No flags set]
    Header types                           [No flags set]
    MAC header fields                      [No flags set]
    Max MAC header filters                 0
    Max queue groups                       0
    Max queues per group                   0
    Min lookahead split size               0
    Max lookahead split size               0
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://msdn.microsoft.com/library/windows/hardware/ff571081)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[WDI 微型端口驱动程序设计指南](https://msdn.microsoft.com/windows/hardware/drivers/network/wdi-miniport-driver-design-guide)

[WDI 微型端口驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/dn926075)

 

 






