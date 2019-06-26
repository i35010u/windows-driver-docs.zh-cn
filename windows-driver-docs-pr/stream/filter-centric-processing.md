---
title: 以筛选器为中心的处理
description: 以筛选器为中心的处理
ms.assetid: e56c5102-7ea6-4687-ae5e-1550db9500f0
keywords:
- 筛选器为中心的筛选器 WDK AVStream
- AVStream 筛选器以筛选器 WDK
- 筛选器类型 WDK AVStream
- AVStrMiniFilterProcess
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1319eeb257a4cd95a05a4a500b52bc8b6c79ee5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384079"
---
# <a name="filter-centric-processing"></a>以筛选器为中心的处理





如果筛选器使用筛选器为中心的处理，则默认情况下，将调用的微型驱动程序提供 AVStream [ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)回调例程时有可用的数据帧的每个插针实例。 微型驱动程序可以通过设置修改此默认行为**标志**的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。

若要实现筛选器为中心的处理，提供指向微型驱动程序提供的指针[ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)中的回调例程**过程**的成员[**KSFILTER\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter_dispatch)结构。 设置**进程**的成员[ **KSPIN\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_dispatch)到**NULL**。

AVStream 调用[ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)仅当所有下列条件满足时：

-   帧是可在需要处理发生的帧的插针上。 微型驱动程序可以通过设置标志来修改处理行为**标志**的成员[ **KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)。 特别注意 KSPIN 互相排斥的标志的组合\_标志\_帧\_不\_必需\_有关\_处理和 KSPIN\_标志\_某些\_帧\_必需\_为\_处理。 微型驱动程序还可以修改的一组 pin 的要求使用帧[ **KsPinAttachAndGate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinattachandgate)或[ **KsPinAttachOrGate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinattachorgate)例程。

-   Pin 实例数是等于或大于**InstancesNecessary**的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。 **ClientState**的成员[ **KSPIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin)结构指定特定[ **KSSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksstate)pin 当前设置的枚举器。 之后**InstancesNecessary**已在满足、 其他 pin **KSSTATE\_停止**状态不会阻止筛选器处理。

-   满足所需的数量的 pin 实例 (如指定的那样**InstancesNecessary**的成员[ **KSPIN\_描述符\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)结构。

-   微型驱动程序使用未关闭筛选器的过程控制门 **KSGATE * * * Xxx*函数。

在中[ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)回调例程，微型驱动程序接收到的数组的指针[ **KSPROCESSPIN\_INDEXENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksprocesspin_indexentry)结构。 AVStream 进行排序的数组 KSPROCESSPIN\_INDEXENTRY 结构通过 pin id。

下面的代码示例演示了如何使用过程 pin 结构。 代码摘自[AVStream 以筛选器为中心的模拟捕获驱动程序 (Avssamp)](https://go.microsoft.com/fwlink/p/?linkid=256084)示例，演示如何编写筛选器以捕获驱动程序。 Windows 驱动程序工具包示例下载中包含源代码和本示例的说明。

微型驱动程序收到的 KSPROCESSPIN 数组\_INDEXENTRY 结构中其筛选器处理调度。 在此示例中，微型驱动程序从中提取的第一个 KSPROCESSPIN 结构 KSPROCESSPIN\_索引视频的 INDEXENTRY 结构\_PIN\_ID:

```cpp
NTSTATUS
CCaptureFilter::
Process (
    IN PKSPROCESSPIN_INDEXENTRY ProcessPinsIndex
    )
{
PKSPROCESSPIN VideoPin = NULL;
...
VideoPin = ProcessPinsIndex [VIDEO_PIN_ID].Pins [0];
...
}
```

微型驱动程序不应引用**ProcessPinsIndex** \[ *n*\]。**Pin** \[0\]它已验证的之前**计数**隶属**ProcessPinsIndex** \[ *n*\]至少一个*或*的**InstancesNecessary** KSPIN 成员\_描述符\_EX中包含的结构**Pin** \[0\]是至少一个。 （如果后者为 true，pin 可确保存在。）

然后，若要指定要捕获的帧，pin [ *AVStrMiniFilterProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksfilterprocess)回调例程将指针传递到到 KSPROCESSPIN 结构*CaptureFrame*、供应商提供捕获例程：

```cpp
VidCapPin -> CaptureFrame (VideoPin, m_Tick);
```

捕获例程可以复制面向或源自**数据**KSPROCESSPIN 结构中的成员。 它还可能会更新**BytesUsed**并**终止**隶属于此结构，如以下示例所示：

```cpp
RtlCopyMemory ( ProcessPin -> Data,
                m_SynthesisBuffer,
                m_VideoInfoHeader -> bmiHeader.biSizeImage
               );
ProcessPin -> BytesUsed = m_VideoInfoHeader -> bmiHeader.biSizeImage;
ProcessPin -> Terminate = TRUE;
```

微型驱动程序还可以访问流标头结构对应于当前流指针和 pin:

```cpp
PKSSTREAM_HEADER StreamHeader = ProcessPin -> StreamPointer -> StreamHeader;
```

使用筛选器以中心处理的大多数微型驱动程序使用流指针仅对标头的流访问。 在筛选器为中心的模型中，AVStream 内部操作流指针。 因此，微型驱动程序应谨慎如果它们操作筛选器为中心的驱动程序中的流指针。
