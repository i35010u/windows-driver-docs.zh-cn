---
title: 硬件事件
description: 硬件事件
ms.assetid: b91e02dd-0de4-4de3-ade6-778339ce47a8
keywords:
- 音频活动 WDK，硬件
- WDM 音频事件 WDK
- 硬件事件 WDK 音频
- 事件 WDK 音频
- 手动控制事件 WDK 音频
- 音量控制事件 WDK 音频
- 静音切换事件 WDK 音频
- 端口驱动程序 WDK 音频，事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6505652340196f9e0bf554e8c184bbcb91aec714
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833351"
---
# <a name="hardware-events"></a>硬件事件


## <span id="hardware_events"></span><span id="HARDWARE_EVENTS"></span>


某些音频设备提供硬件卷控制旋钮、静音开关或其他类型的手动控制。 应用程序可以通过调整音量或更改音频流的播放方式来响应这些控件中的更改。 当用户调整硬件控制时，微型端口驱动程序使用[IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents)接口来通知端口驱动程序硬件事件已发生。 然后，端口驱动程序会向应用程序通知事件，使其可以从设备读取新的控制设置。

小型端口驱动程序可在服务**Init**调用时查询**IPortEvents**接口的端口驱动程序（例如，请参阅[**IMiniportWavePci：： Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)）。 在 Microsoft Windows 98 SE、Windows Me 和 Windows 2000 及更高版本上，该查询将成功。 有关代码示例，请参阅 Windows 驱动程序工具包（WDK）中的 Sb16 示例音频适配器。

当端口驱动程序调用你的驱动程序的[**IMiniport：： GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)方法时，该方法会输出一个[**PCFILTER\_说明符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)结构，该结构指定你的设备支持的事件，其中包括其他内容。 可以在自动化表中为 PCFILTER\_描述符的**pin**和**节点**成员指定事件，并在**AutomationTable**成员中指定事件，这些事件指向筛选器本身的自动化表。 每个事件都由[**PCEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item)结构指定。 你的驱动程序应将 PCEVENT\_项结构的**set**和**Id**成员设置为[KSEVENTSETID\_AudioControlChange](https://docs.microsoft.com/windows-hardware/drivers/audio/kseventsetid-audiocontrolchange)和[**KSEVENT\_控件\_更改**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-control-change)，并应将指针加载到驱动程序的[**EventHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler)例程导入**处理程序**成员。 您的驱动程序还应将 PCEVENT\_项\_标志设置为**Flags**成员中\_BASICSUPPORT 位以指示对控件更改事件的基本支持，并应将 PCEVENT\_项设置\_标志\_ONESHOT 和/或 PCEVENT\_项\_标志\_启用位以指示它支持一次的通知和/或定期通知。

当应用程序稍后调用**mixerOpen**函数（如 Microsoft Windows SDK 文档中所述）来请求特定事件的通知时，端口驱动程序将使用指向 [**PCEVENT\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)结构。 此结构的**谓词**成员设置为 PCEVENT\_谓词\_ADD，其**EventItem**成员指定要启用的事件。 PCEVENT\_请求结构还包含指向[**KSEVENT\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksevent_entry)结构的指针，驱动程序应将此结构视为不透明的系统数据。 启用事件后，处理程序应调用具有相同 KSEVENT\_入口指针的[**IPortEvents：： AddEventToEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist) 。 通过此调用，处理程序将确认事件已启用。

当发生硬件事件并且驱动程序的中断服务例程检测到静音或卷更改时，你的驱动程序通过使用一组描述事件的参数调用[**IPortEvents：： GenerateEventList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist)来向端口驱动程序发送信号。 例如，下面的调用描述了 lineout 节点中的控件更改：

```cpp
    pPE->GenerateEventList(NULL, KSEVENT_CONTROL_CHANGE,
                           FALSE, ULONG(-1), TRUE, LINEOUT_VOL);
```

在此调用期间，端口驱动程序会在其事件列表中搜索与 call 参数匹配的所有事件，并将通知发送到监视这些事件的客户端。 在此示例中，pPE 是指向**IPortEvents**对象的指针，而 LINEOUT\_VOL 是微型端口驱动程序分配给 LINEOUT 节点的节点 ID。 未指定的参数（例如前面示例中的事件集 GUID 和 pin ID）被视为通配符，并始终与列表中的相应参数匹配。

 

 




