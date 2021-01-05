---
title: 硬件事件
description: 硬件事件
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
ms.openlocfilehash: cc57a6ebcb3754016843d3de0e914f1cac8c7378
ms.sourcegitcommit: 7bdf85c72841fbc2093c315f900c69d2eef6e3e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2020
ms.locfileid: "97757869"
---
# <a name="hardware-events"></a>硬件事件


## <span id="hardware_events"></span><span id="HARDWARE_EVENTS"></span>


某些音频设备提供硬件卷控制旋钮、静音开关或其他类型的手动控制。 应用程序可以通过调整音量或更改音频流的播放方式来响应这些控件中的更改。 当用户调整硬件控制时，微型端口驱动程序使用 [IPortEvents](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportevents) 接口来通知端口驱动程序硬件事件已发生。 然后，端口驱动程序会向应用程序通知事件，使其可以从设备读取新的控制设置。

小型端口驱动程序可在服务 **Init** 调用时查询 **IPortEvents** 接口的端口驱动程序 (参阅 [**IMiniportWavePci：： Init**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)，例如从端口驱动程序) 。 在 Microsoft Windows 98 SE、Windows Me 和 Windows 2000 及更高版本上，该查询将成功。 有关代码示例，请参阅 Windows 驱动程序工具包的早期版本中的 Sb16 示例音频适配器 (WDK) 。

当端口驱动程序调用你的驱动程序的 [**IMiniport：： GetDescription**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription) 方法时，该方法会输出一个 [**PCFILTER \_ 说明符**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor) 结构，该结构指定你的设备支持的事件，以及其他所有内容。 可以在自动化表中为 PCFILTER 描述符的 **引脚** 和 **节点** 成员指定事件， \_ 并在 **AutomationTable** 成员中指定事件，这些事件指向筛选器本身的自动化表。 每个事件都由 [**PCEVENT \_ 项**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcevent_item) 结构指定。 你的驱动程序应将 PCEVENT \_ 项结构 **的 Set** 和 **Id** 成员设置为 [KSEVENTSETID \_ AudioControlChange](./kseventsetid-audiocontrolchange.md) 和 [**KSEVENT \_ 控件 \_ 更改**](./ksevent-control-change.md)，并应将指向驱动程序的 [**EventHandler**](/windows-hardware/drivers/ddi/portcls/nc-portcls-pcpfnevent_handler) 例程的指针加载到 **处理程序** 成员。 你的驱动程序还应将 \_ \_ Flags 成员中的 PCEVENT ITEM 标志 \_ BASICSUPPORT 位设置为指示对控件更改事件的基本支持，并应设置 PCEVENT \_ 项 \_ 标志 \_ ONESHOT 和/或 PCEVENT \_ item \_ 标志， \_ 以使 bits 能够指示它支持一次拍摄和/或重复的通知。

当应用程序稍后调用 Microsoft Windows SDK 文档) 中描述 (**mixerOpen** 函数来请求特定事件的通知时，端口驱动程序将使用指向 [**PCEVENT \_ 请求**](/windows-hardware/drivers/ddi/portcls/ns-portcls-_pcevent_request)结构的指针调用驱动程序的 **EventHandler** 例程。 此结构的 **谓词** 成员设置为 PCEVENT \_ verb \_ ADD，其 **EventItem** 成员指定要启用的事件。 PCEVENT \_ 请求结构还包含指向您的驱动程序应视为不透明系统数据的 [**KSEVENT \_ 条目**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksevent_entry) 结构的指针。 启用事件后，处理程序应将 [**IPortEvents：： AddEventToEventList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-addeventtoeventlist) 与相同的 KSEVENT \_ 项指针一起调用。 通过此调用，处理程序将确认事件已启用。

当发生硬件事件并且驱动程序的中断服务例程检测到静音或卷更改时，你的驱动程序通过使用一组描述事件的参数调用 [**IPortEvents：： GenerateEventList**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportevents-generateeventlist) 来向端口驱动程序发送信号。 例如，下面的调用描述了 lineout 节点中的控件更改：

```cpp
    pPE->GenerateEventList(NULL, KSEVENT_CONTROL_CHANGE,
                           FALSE, ULONG(-1), TRUE, LINEOUT_VOL);
```

在此调用期间，端口驱动程序会在其事件列表中搜索与 call 参数匹配的所有事件，并将通知发送到监视这些事件的客户端。 在此示例中，pPE 是指向 **IPortEvents** 对象的指针，而 LINEOUT \_ VOL 是小型端口驱动程序分配给 LINEOUT 节点的节点 ID。 未指定的参数 (例如前面示例中的事件集 GUID 和 pin ID) 会视为通配符，并始终与列表中的相应参数匹配。

 

