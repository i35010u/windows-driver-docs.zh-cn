---
title: 以筛选器为中心的处理
description: 以筛选为中心的处理
keywords:
- 以筛选为中心的筛选器 WDK AVStream
- AVStream 筛选器-中心筛选器 WDK
- 筛选器类型 WDK AVStream
- AVStrMiniFilterProcess
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: fee7f58cb8dae351a147e414c5c2d1925e540440
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837873"
---
# <a name="filter-centric-processing"></a>以筛选为中心的处理

如果筛选器使用以筛选方式为中心的处理，则默认情况下，AVStream 在每个 pin 实例上都有可用的数据帧时调用微型驱动程序提供的 [*AVStrMiniFilterProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess) 回调例程。 微型驱动程序可以通过设置 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的 **Flags** 成员来修改此默认行为。

若要实现以筛选为中心的处理，请提供一个指针，该指针指向 [**KSFILTER \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_dispatch)结构的 **进程** 成员中微型驱动程序提供的 [*AVStrMiniFilterProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess)回调例程。 将 [**KSPIN \_ 调度**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_dispatch)的 **进程** 成员设置为 **NULL**。

仅当满足以下所有条件时，AVStream 才会调用 [*AVStrMiniFilterProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess) ：

- 需要帧才能进行处理的 pin 上提供了帧。 微型驱动程序可以通过在 KSPIN 描述符的 **flags** 成员（ [**\_ \_ 例如**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)）中设置标志来修改处理行为。 特别要注意的是，处理和 KSPIN 不需要的相互排斥的标志 KSPIN \_ 标志帧的组合 \_ \_ 会 \_ \_ \_ \_ 标记 \_ \_ \_ 处理所需的某些帧 \_ \_ 。 微型驱动程序还可以通过使用 [**KsPinAttachAndGate**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachandgate) 或 [**KsPinAttachOrGate**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinattachorgate) 例程来修改需要帧的 pin 集。

- Pin 实例数等于或大于 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的 **InstancesNecessary** 成员。 [**KSPIN**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)结构的 **ClientState** 成员指定当前设置了 pin 的特定 [**KSSTATE**](/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)枚举器。 满足 **InstancesNecessary** 后， **KSSTATE \_ 停止** 状态中的其他 pin 将不会阻止筛选器处理。

- 满足 [**KSPIN \_ 描述符 \_ EX**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)结构的 **InstancesNecessary** 成员所指定 (所需的 pin 实例数量。

- 微型驱动程序尚未使用 **KSGATE**_Xxx_ 函数关闭筛选器的处理控制入口。

在 [*AVStrMiniFilterProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess) 回调例程中，微型驱动程序接收指向 [**KSPROCESSPIN \_ INDEXENTRY**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksprocesspin_indexentry) 结构的数组的指针。 AVStream \_ 按 PIN ID 对 KSPROCESSPIN INDEXENTRY 结构的数组进行排序。

下面的代码示例演示如何使用处理 pin 结构。 此代码取自 [AVStream Filter-Centric 模拟捕获驱动程序 (Avssamp) ](/samples/microsoft/windows-driver-samples/avstream-filter-centric-simulated-capture-sample-driver-avssamp/) 示例，该示例演示如何编写以筛选为中心的捕获驱动程序。 Windows 驱动程序工具包示例下载中提供了本示例的源代码和说明。

微型驱动程序 \_ 在其筛选器进程调度中接收 KSPROCESSPIN INDEXENTRY 结构的数组。 在此示例中，微型驱动程序从 \_ 索引视频 PIN ID 的 KSPROCESSPIN INDEXENTRY 结构中提取第一个 KSPROCESSPIN 结构 \_ \_ ：

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

微型驱动程序不应引用 **ProcessPinsIndex** \[ *n* \] 。**Pins** \[ \] 在验证 **ProcessPinsIndex** n 的 **Count** 成员 \[ *n* \] 是至少一个之前，*或* 在 **InstancesNecessary** \_ \_ **引脚** 0 中包含的 KSPIN 描述符 EX 结构的 InstancesNecessary 成员 \[ \] 至少为1的情况下，0针0。  (如果后者为 true，则保证 pin 存在。 ) 

然后，若要指定捕获帧的 pin， [*AVStrMiniFilterProcess*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnksfilterprocess) 回调例程会将指向 KSPROCESSPIN 结构的指针传递到 *CaptureFrame*，即供应商提供的捕获例程：

```cpp
VidCapPin -> CaptureFrame (VideoPin, m_Tick);
```

然后，捕获例程可以复制到 KSPROCESSPIN 结构的 **数据** 成员或从中复制数据。 它还可以更新 **BytesUsed** 并 **终止** 此结构的成员，如以下示例中所示：

```cpp
RtlCopyMemory ( ProcessPin -> Data,
                m_SynthesisBuffer,
                m_VideoInfoHeader -> bmiHeader.biSizeImage
               );
ProcessPin -> BytesUsed = m_VideoInfoHeader -> bmiHeader.biSizeImage;
ProcessPin -> Terminate = TRUE;
```

微型驱动程序还可以访问与当前流指针和 pin 对应的流标头结构：

```cpp
PKSSTREAM_HEADER StreamHeader = ProcessPin -> StreamPointer -> StreamHeader;
```

使用以筛选器为中心的处理的大多数微型驱动程序只使用流指针进行流头访问。 在以筛选为中心的模型中，AVStream 在内部处理流指针。 因此，如果微型驱动程序在以筛选器为中心的驱动程序中操作流指针，则应小心操作。
