---
title: 在 AVStream 编解码器中支持动态格式更改
description: 在 AVStream 编解码器中支持动态格式更改
ms.assetid: ae222512-fd19-404a-aaf8-6fbfa2a3349e
keywords:
- 硬件编解码器支持 WDK AVStream，动态格式更改
- 支持动态格式更改 WDK AVStream
- 动态格式更改 WDK AVStream
- AVStream 硬件编解码器支持 WDK，支持动态格式更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc5beaad8ab5fa95cbde4823680775446ff6d8ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837666"
---
# <a name="supporting-dynamic-format-changes-in-avstream-codecs"></a>在 AVStream 编解码器中支持动态格式更改


如果在运行的媒体流中发生动态格式更改，则系统提供的 Devproxy 模块将与捕获 pin 协商，以确定是否可接受新格式。

从媒体源产生动态格式更改时，会发生以下事件序列：

1.  驱动程序将接收[**KSPROPERTY\_连接\_PROPOSEDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-proposedataformat)请求，以确定输入 KS pin 是否支持新的媒体类型。 驱动程序必须支持此属性。

2.  如果输入插针支持新媒体类型，则 KSPROPERTY\_连接\_PROPOSEDATAFORMAT 处理程序应返回\_成功的状态。 然后，该驱动程序会通过将建议的输入与当前选择的输出媒体类型一起使用来确定它是否可以恢复流。 如果是，则流继续。

3.  如果输入插针不支持新建议的媒体类型，则 KSPROPERTY\_连接\_PROPOSEDATAFORMAT 处理程序应返回错误。 然后，HW MFT 用连接的组件重新协商媒体类型。

4.  如果输入插针支持新的媒体输入类型，但 KS 筛选器需要不同的输出媒体类型，则驱动程序应生成[**KSEVENT\_动态\_格式\_更改**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-dynamic-format-change)事件，如本主题后面所述，通知 HW MFT媒体类型更改。

5.  当 HW MFT 收到 KSEVENT 通知时，会将输出插针从**KSSTATE\_运行**转换为 KSSTATE\_停止。

6.  然后，HW MFT 会查询驱动程序中可用的媒体类型，转换为对驱动程序的[*AVStrMiniIntersectHandlerEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnksintersecthandlerex)交集处理程序的调用。 驱动程序应按照优先顺序报告首选输出媒体类型。

7.  用户模式客户端选择媒体类型，并在 HW MFT 的输出插针上设置新的媒体类型。 这将导致对驱动程序的[*AVStrMiniPinSetDataFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat)调度例程的调用。 如果驱动程序通过返回状态\_"成功" 来接受格式，则使用新的媒体类型恢复流。 如果调用失败，格式更改所涉及的组件必须重新协商媒体类型。

8.  HW MFT 检查连接介质中是否有任何变化。 如果没有更改，它将在 pin 上设置选定的媒体类型，并将其放入 KSSTATE\_运行。 如果连接介质发生更改，则 HW MFT 会销毁该 pin，并使用新选择的介质类型和介质重新创建它。 然后，MFT\_运行，然后将 pin 放入 KSSTATE。

9.  流式处理恢复。

在某些情况下，媒体源可能检测不到格式更改。 例如，MPEG2 解码器必须解码每个数据包，才能发现任何格式更改。

在这种情况下，如果驱动程序检测到格式更改，则硬件驱动程序应生成动态格式更改 KSEVENT。 然后，HW MFT 会查询 pin 以查找其受支持的媒体类型。 Pin 应按照优先顺序返回首选的媒体类型。 然后，HW MFT 按照上一部分的步骤4到步骤9中所述的事件顺序进行。

如果驱动程序无法处理此类格式更改，它应该返回流式处理错误，然后传播到 MF。

下面的代码示例演示如何使用 KSEVENT 定义新的动态格式更改：

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

每个 pin 应在其 pin 描述符中公开此事件。 事件的类型为 KSEVENTF\_事件\_句柄。

驱动程序生成此事件之前，应根据当前所选的输入媒体类型设置 KS pin 的首选媒体类型。 为此，可以[ **\_使用 KsEdit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-_ksedit)函数来处理 pin 的描述符。

为了生成事件，驱动程序应调用[**KsGenerateEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksgenerateevents)。

 

 




