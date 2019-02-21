---
title: 在 AVStream 编解码器支持动态格式更改
description: 在 AVStream 编解码器支持动态格式更改
ms.assetid: ae222512-fd19-404a-aaf8-6fbfa2a3349e
keywords:
- 硬件编解码器支持 WDK AVStream，动态格式更改
- 支持动态格式更改 WDK AVStream
- 动态格式更改 WDK AVStream
- AVStream 硬件编解码器支持 WDK，支持动态格式更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 030d22c07134ede6ea81131f30d783c3bbc452e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543627"
---
# <a name="supporting-dynamic-format-changes-in-avstream-codecs"></a>在 AVStream 编解码器支持动态格式更改


正在运行的媒体流动态格式更改时，系统提供 Devproxy 模块协商使用捕获的 pin 来确定是否将可接受新的格式。

当动态格式更改是从媒体源时，会发生以下事件序列：

1.  驱动程序收到[ **KSPROPERTY\_连接\_PROPOSEDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff565107)请求以确定输入 KS pin 是否支持新的媒体类型。 驱动程序必须支持此属性。

2.  输入插针是否支持新的媒体类型，KSPROPERTY\_连接\_PROPOSEDATAFORMAT 处理程序应返回状态\_成功。 然后，该驱动程序确定它是否可以使用当前所选的输出的媒体类型以及建议的输入来恢复流。 如果是，流将恢复。

3.  如果输入插针不支持的新建议的媒体类型，KSPROPERTY\_连接\_PROPOSEDATAFORMAT 处理程序应返回一个错误。 HW MFT 然后重新连接组件使用的媒体类型进行协商。

4.  如果输入插针支持新的媒体输入的类型，但 KS 筛选器需要不同的输出媒体类型，则驱动程序应生成[ **KSEVENT\_动态\_格式\_更改**](https://msdn.microsoft.com/library/windows/hardware/ff561849)事件，如本主题，以通知有关媒体类型更改 HW MFT 更高版本中所述。

5.  如果硬件 MFT 接收 KSEVENT 通知时，它将转换的输出插针**KSSTATE\_运行**到 KSSTATE\_停止。

6.  HW MFT 然后查询驱动程序对于可用的媒体类型，这会转换为对驱动程序的调用[ *AVStrMiniIntersectHandlerEx* ](https://msdn.microsoft.com/library/windows/hardware/ff556326)交集处理程序。 该驱动程序应报告按偏好顺序列出的首选的输出媒体类型。

7.  用户模式下客户端选择媒体类型，并将新的媒体类型设置的 HW MFT 输出插针上。 这会导致驱动程序的调用[ *AVStrMiniPinSetDataFormat* ](https://msdn.microsoft.com/library/windows/hardware/ff556355)调度例程。 如果该驱动程序接受格式通过返回状态\_成功时，流式处理与新的媒体类型的恢复。 如果调用失败，则格式更改中涉及的组件必须重新协商媒体类型。

8.  HW MFT 检查是否已连接的介质中的任何更改。 如果没有任何更改，它在针上设置的所选的媒体类型，并将其放入 KSSTATE\_运行。 如果在已连接的介质中的更改，HW MFT 销毁 pin，并将其与新选择的媒体类型和介质重新创建。 MFT 然后将 pin 放入 KSSTATE\_运行。

9.  继续进行流式处理。

在某些情况下，媒体源可能无法检测格式更改。 例如，必须 MPEG2 解码器解码每个数据包，若要查找任何格式更改。

在这种情况下，如果该驱动程序检测到格式更改，硬件驱动程序应生成动态格式更改 KSEVENT。 然后，HW MFT 查询其支持的媒体类型的 pin。 Pin 应返回按偏好顺序列出的首选的媒体类型。 HW MFT 然后遵循步骤 4 到 9 的上一节中所述的事件的顺序。

如果该驱动程序无法处理此类格式更改，则应返回一个流式处理的错误，然后传播到 MF。

下面的代码示例演示如何通过使用 KSEVENT 定义新的动态格式更改：

```cpp
// {162AC456-83D7-4239-96DF-C75FFA138BC6}
#define STATIC_KSEVENTSETID_DynamicFormatChange\
    0x162ac456, 0x83d7, 0x4239, 0x96, 0xdf, 0xc7, 0x5f, 0xfa, 0x13, 0x8b, 0xc6 DEFINE_GUIDSTRUCT("162AC456-83D7-4239-96DF-C75FFA138BC6", KSEVENTSETID_ DynamicFormatChange);
#define KSEVENTSETID_DynamicFormatChange DEFINE_GUIDNAMED(KSEVENTSETID_ DynamicFormatChange)

typedef enum {
KSEVENT_DYNAMIC_FORMAT_CHANGE = 0
};

DEFINE_KSEVENT_TABLE(DynamicFormatChangeEventTable) {
    DEFINE_KSEVENT_ITEM
    (
        KSEVENT_DYNAMIC_FORMAT_CHANGE,
        sizeof(KSEVENTDATA),
        0,   
        NULL,
        NULL,
        NULL
    )
};

KSEVENT_SET PinEventTable[] =
{
    DEFINE_KSEVENT_SET
    (
        &KSEVENTSETID_DynamicFormatChange,
        SIZEOF_ARRAY(DynamicFormatChangeEventTable),
        DynamicFormatChangeEventTable
    )
};
```

每个 pin 应公开此事件在其 pin 描述符。 事件属于类型 KSEVENTF\_事件\_处理。

驱动程序将生成此事件之前，它应设置基于当前所选的输入的媒体类型 KS 刻度格的首选的媒体类型。 您可以执行此操作通过使用[  **\_KsEdit** ](https://msdn.microsoft.com/library/windows/hardware/ff568796)插针的描述符上的函数。

若要生成该事件，驱动程序应调用[ **KsGenerateEvents**](https://msdn.microsoft.com/library/windows/hardware/ff562597)。

 

 




