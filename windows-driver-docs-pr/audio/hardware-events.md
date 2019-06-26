---
title: 硬件事件
description: 硬件事件
ms.assetid: b91e02dd-0de4-4de3-ade6-778339ce47a8
keywords:
- 音频事件 WDK，硬件
- WDM 音频事件 WDK
- 硬件事件 WDK 音频
- 事件 WDK 音频
- 手动控制事件 WDK 音频
- 音量控制事件 WDK 音频
- 静音开关事件 WDK 音频
- 端口驱动程序 WDK 音频，事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e6884994244d9ef73f187eae05af53ce94c19c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360006"
---
# <a name="hardware-events"></a>硬件事件


## <span id="hardware_events"></span><span id="HARDWARE_EVENTS"></span>


一些音频设备提供硬件音量控制旋钮、 静音开关或其他类型的手动控件。 应用程序可以通过调节音量或更改播放的音频流的方式响应这些控件中的更改。 当用户调整硬件控制时，微型端口驱动程序使用[IPortEvents](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportevents)接口来通知发生了硬件事件端口驱动程序。 端口驱动程序，反过来，通知事件的应用程序，以便它可以从设备中读取新的控制设置。

微型端口驱动程序可以查询的端口驱动程序**IPortEvents**在其提供服务时的接口**Init**调用 (请参阅[ **IMiniportWavePci::Init** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-init)，例如) 从端口驱动程序。 在 Microsoft Windows 98 SE、 Windows Me 和 Windows 2000 及更高版本，该查询会成功。 有关代码示例，请参阅 Sb16 示例音频适配器 Windows Driver Kit (WDK) 中。

当端口驱动程序调用您的驱动程序[ **IMiniport::GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-getdescription)方法，该方法输出[ **PCFILTER\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor)结构，它指定，除此之外，你的设备支持的事件。 可以自动化的表中指定事件**插针**并**节点**PCFILTER 成员\_描述符，然后在**AutomationTable**成员，它指向的筛选器本身的自动化表。 指定每个事件[ **PCEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcevent_item)结构。 您的驱动程序应设置 PCEVENT\_项结构**设置**并**Id**成员[KSEVENTSETID\_AudioControlChange](https://docs.microsoft.com/windows-hardware/drivers/audio/kseventsetid-audiocontrolchange)和[**KSEVENT\_控制\_更改**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-control-change)，并应加载到您的驱动程序的指针[ **EventHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nc-portcls-pcpfnevent_handler)到日常**处理程序**成员。 您的驱动程序还应设置 PCEVENT\_项\_标志\_BASICSUPPORT 位**标志**成员来指示基本支持的控件更改事件，并且它应设置 PCEVENT\_项\_标志\_ONESHOT 和/或 PCEVENT\_项\_标志\_启用 bits 以指示它支持单步和/或定期通知。

当应用程序更高版本调用**mixerOpen**请求通知的特定事件，然后该端口驱动程序 （Microsoft Windows SDK 文档中所述） 的函数将调用您的驱动程序**事件处理程序**例程的指针替换[ **PCEVENT\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-_pcevent_request)结构。 此结构**谓词**成员设置为 PCEVENT\_谓词\_添加并将其**EventItem**成员指定是启用的事件。 PCEVENT\_请求结构还包含指向的指针[ **KSEVENT\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksevent_entry)您的驱动程序应将视为不透明的系统数据的结构。 在启用该事件之后, 您的处理程序应调用[ **IPortEvents::AddEventToEventList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportevents-addeventtoeventlist)使用相同 KSEVENT\_条目指针。 凭借此调用，该处理程序确认该事件已启用。

硬件事件发生时您的驱动程序的中断服务例程检测到静音或量的变化，您的驱动程序通过调用向端口驱动程序的事件发出信号[ **IPortEvents::GenerateEventList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportevents-generateeventlist)与一组描述该事件的参数。 例如，以下调用说明线路输出音量节点中的控件更改：

```cpp
    pPE->GenerateEventList(NULL, KSEVENT_CONTROL_CHANGE,
                           FALSE, ULONG(-1), TRUE, LINEOUT_VOL);
```

此调用期间端口驱动程序搜索与调用参数匹配的所有事件及其事件列表，并将通知发送到客户端监视这些事件的。 在此示例中，pPE 是指向**IPortEvents**对象和线路输出\_期是微型端口驱动程序将分配给线路输出卷节点的节点 ID。 未指定的参数 （如的事件集 GUID 和前面的示例中的 pin ID） 将被视为通配符，并始终匹配列表中的相应参数。

 

 




