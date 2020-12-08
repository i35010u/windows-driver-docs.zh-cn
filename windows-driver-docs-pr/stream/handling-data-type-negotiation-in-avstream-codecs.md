---
title: 在 AVStream 编解码器中处理数据类型协商
description: 在 AVStream 编解码器中处理数据类型协商
keywords:
- 硬件编解码器支持 WDK AVStream，数据类型协商
- 数据类型协商 WDK AVStream
- AVStream 硬件编解码器支持 WDK，处理数据类型协商
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e54322e7c5e9a52eecb4311724b55e5cc59b436
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815829"
---
# <a name="handling-data-type-negotiation-in-avstream-codecs"></a>在 AVStream 编解码器中处理数据类型协商

初始化设备时，系统提供的设备代理 (Devproxy) 模块解析驱动程序提供的筛选器描述符。 此外，Devproxy 会公开相应 MFT 的输入插针和输出插针上的驱动程序支持的数据范围 (媒体基础转换) 。

流式处理开始时，MF 管道和用户模式应用程序使用这些范围来对驱动程序进行数据类型协商。

在数据类型协商过程中，会发生下列交互：

1. Devproxy 检索硬件编解码器筛选器的每个 pin 描述符中的微型驱动程序提供的数据范围。

1. Devproxy 发出对驱动程序的数据交集请求。

1. Devproxy 向 MF 公开格式完全相同的类型。

1. MF 拓扑生成器 (的 MF 等效于 DirectShow 图形生成器) 构造流拓扑。

1. 在 MF 拓扑生成器为 Devproxy 输入/输出插针完成数据类型后，它将通过调用微型驱动程序的 [*AVStrMiniPinSetDataFormat*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspinsetdataformat) 回调函数来设置 pin 上的数据类型。 如果 KS pin 不存在，Devproxy 将调用 [**KsCreatePin**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatepin)。

若要启用成功的数据类型协商，微型驱动程序必须执行以下步骤：

1. 为硬件编解码器筛选器中包含的每个公开的 pin，在 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)的 **DataRanges** 成员中提供受支持的数据范围列表。 例如：

    ```cpp
    const PKSDATARANGE VideoDecoderInputPinDataRanges[8] = {
        (PKSDATARANGE)&H264DataFormat,
        (PKSDATARANGE)&VC_1DataFormat,
        (PKSDATARANGE)&VC_1DataFormatVIH2,
        (PKSDATARANGE)&WMV9DataFormat,
        (PKSDATARANGE)&WMV9DataFormatVIH2,
        (PKSDATARANGE)&DX50DataFormat,
        (PKSDATARANGE)&DX50DataFormatVIH2,
        (PKSDATARANGE)&MPEG2DataFormat
    };
    ```

    在这种情况下，指定的范围为包装类型，例如 [**ks \_ DATARANGE \_ MPEG2 \_ 视频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_mpeg2_video)、 [**ks \_ DATARANGE \_ 视频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)和 [**ks \_ DATARANGE \_ VIDEO2**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video2)。 在前面列出的代码示例中，每个范围都是转换到 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85))。

    包装结构的最后一个成员称为格式块结构，例如 KS \_ DATARANGE \_ MPEG2 \_ 视频。**VideoInfoHeader**。

    支持连续数据区域的驱动程序应指定格式块结构中的最大值。 支持离散数据范围的驱动程序应指定包含格式块结构中离散值的数组。

    如果以后声明支持给定格式的驱动程序失败，则可能降低性能。 仅可保证支持的列表格式。

1. 驱动程序应允许在 KSSTATE \_ STOP/KSSTATE 运行时在 pin 上设置媒体类型 \_ 。 除了之外，不需要执行任何操作，以确保该驱动程序不会禁止此操作。

1. 驱动程序应在 KSPIN 描述符中提供交集处理程序， [**\_ \_ 如**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex)**IntersectHandler** 每个 pin 的 IntersectHandler。

1. 微型驱动程序应提供 [**KSPROPERTY \_ 连接 \_ PROPOSEDATAFORMAT**](./ksproperty-connection-proposedataformat.md) 属性的处理程序。

1. 如果设置了输出媒体类型，则编码器应根据指定的输出媒体类型使用 pin 描述符) 来报告可能的输入类型 (。 如果未设置输出媒体类型，则编码器不应报告任何输入媒体类型。

1. 如果设置了输入媒体类型，则解码器应根据指定的输入媒体类型报告可能的输出类型。

1. 如果设置了输入媒体类型，则视频处理器应根据指定的输入媒体类型报告其输出类型。

1. 驱动程序应支持 [ICodecAPI](/previous-versions/ms784893(v=vs.85)) 接口。 然后，用户模式组件可以使用此用户模式接口获取编解码器配置信息。

1. 在编码器的设置过程中，首先设置 ICodecAPI 属性，后跟输出媒体类型。 在此之后，编码器只应提供它可以通过当前配置支持的输入类型。

1. **ICodecAPI** 属性和编解码器 API 媒体类型属性在某些区域中重叠，例如，配置文件和级别。 在这些情况下，与媒体类型 "重写" ICodecAPI 属性相关的编解码器 API 属性。 设置介质类型后，微型驱动程序不应允许修改这些重叠属性。

1. 在安装解码器期间，将首先设置输入类型。 在此之后，解码器只应提供它可支持的输出类型及其当前输入类型。

1. 编码器的预期输入应为4:2:0，且至少为 NV12 交错/渐进。 预期输出是格式 MPEG2 PS/p 或 H-p 附录 B 的压缩基本流。

1. 解码器的预期输入是基本流。 预期输出为未压缩的源流的未缩放版本 NV12。

1. AVStream 驱动程序的 pin 应具有相互独立的状态。 这意味着，在输出 pin 仍处于 **KSSTATE \_ 停止** 状态时，输入插针可以从 **KSSTATE \_ 停止** 切换到 **KSSTATE \_ 运行**。

1. 当微型驱动程序接收到带有可变数据缓冲区大小的属性 GET 请求时，微型驱动程序应将 **NULL** 缓冲区解释为所需缓冲区大小的查询。 在这种情况下，驱动程序应在 IoStatus 字段中指定所需的长度 &gt; 并返回状态 \_ 缓冲区 \_ 溢出。 此外，微型驱动程序应将返回代码设置为警告而不是错误。 例如，对数据交集处理程序遵循此指南。
