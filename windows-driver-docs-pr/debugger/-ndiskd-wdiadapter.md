---
title: ndiskd.wdiadapter
description: Ndiskd. wdiadapter 扩展显示有关 WDIWiFi CAdapter 结构的信息。 如果运行不带任何参数的扩展，ndiskd 将显示所有 WDIWiFi CAdapter 结构的列表。
ms.assetid: 1AC069E8-CF87-459B-9C56-DDC1A6F765A8
keywords:
- ndiskd wdiadapter Windows 调试
ms.date: 06/26/2020
topic_type:
- apiref
api_name:
- ndiskd.wdiadapter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ddfa77f65dc81ec5b75b0b6d4b1be426219b6d8b
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593827"
---
# <a name="ndiskdwdiadapter"></a>!ndiskd.wdiadapter

**！ Ndiskd wdiadapter**扩展显示有关 WDIWiFi 的信息！CAdapter 结构。 如果运行不带参数的扩展，！ ndiskd 将显示所有 WDIWiFi 的列表！CAdapter 结构。

有关 WDI 微型端口驱动程序的详细信息，请参阅[WDI 微型端口驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)。

有关 WDI 微型端口驱动程序参考的详细信息，请参阅[WDI 微型端口驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

```console
!ndiskd.wdiadapter [-handle <x>] [-pm] [-rcvfilter] 
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
CAdapter 对象的可选句柄。

<span id="_______-pm______"></span><span id="_______-PM______"></span>*-pm*   
显示电源管理状态和功能。

<span id="_______-rcvfilter______"></span><span id="_______-RCVFILTER______"></span>*-rcvfilter*   
显示接收筛选功能。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

运行不带参数的 **！ ndiskd wdiadapter**扩展，以查看所有 CAdapter 对象的列表以及其每个 WDI 适配器的详细信息。 在下面的示例中，只有一个 CAdapter 结构。 其关联的 WDI 适配器的句柄为 ffffc804af396000。

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

现在，你可以单击 CAdapter 结构说明底部的 "电源管理" 和 "接收筛选" 链接，或者可以输入包含 *-pm*或 *-rcvfilter*选项的 **！ ndiskd**命令。 下面的示例显示了 *-rcvfilter*选项的输出。

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

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd.dll）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[WDI 微型端口驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-miniport-driver-design-guide)

[WDI 微型端口驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
