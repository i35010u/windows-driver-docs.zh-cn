---
title: 在 AVStream 编解码器中处理数据类型协商
description: 在 AVStream 编解码器中处理数据类型协商
ms.assetid: b5212429-dbc8-4e9a-b5a9-2431f8a1eb2a
keywords:
- 硬件编解码器支持 WDK AVStream，数据类型协商
- 数据类型协商 WDK AVStream
- AVStream 硬件编解码器支持 WDK，处理数据类型协商
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5edacb66f45537baf480a3ac2c86f40e9227fc8d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384054"
---
# <a name="handling-data-type-negotiation-in-avstream-codecs"></a>在 AVStream 编解码器中处理数据类型协商

初始化设备时，系统提供设备代理 (Devproxy) 模块将分析驱动程序提供的筛选器描述符。 此外，Devproxy 公开相应的 MFT （媒体基础转换） 的输入和输出插针上的驱动程序支持的数据范围。

流式处理开始时，MF 管道和用户模式应用程序使用这些范围执行使用驱动程序的数据类型协商。

数据类型协商期间发生以下交互：

1.  Devproxy 检索由硬件编解码器筛选器的每个 pin 描述符中微型驱动程序提供的数据范围。

2.  Devproxy 向驱动程序发出数据交集请求。

3.  Devproxy 公开到 MF 完全正确的类型。

4.  MF 拓扑生成器 （MF 相当于 DirectShow 图生成器） 构造流式处理拓扑。

5.  MF 拓扑生成器完成 Devproxy 输入/输出插针的数据类型后，它设置的数据类型在针上通过调用微型驱动程序的[ *AVStrMiniPinSetDataFormat* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspinsetdataformat)回调函数。 如果 KS pin 不存在，调用 Devproxy [ **KsCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatepin)。

若要启用成功的数据类型协商，微型驱动程序必须执行以下步骤：

1.  提供一系列中的受支持的数据范围**DataRanges**的成员[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)硬件编解码器筛选器中包含每个公开 pin。 例如：

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

    在这种情况下，指定的范围都是包装器类型如[ **KS\_DATARANGE\_MPEG2\_视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_mpeg2_video)， [ **KS\_DATARANGE\_视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video)，并[ **KS\_DATARANGE\_视频 2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_datarange_video2)。 在前面列出的代码示例中，每个范围进行类型转换到[ **KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))。

    包装结构的最后一个成员称为格式块结构，例如，KS\_DATARANGE\_MPEG2\_视频。**VideoInfoHeader**。

    支持连续数据区域的驱动程序应指定格式的块结构中的最大值。 支持离散数据范围的驱动程序应指定一个包含格式块结构中的离散值的数组。

    如果声明，以便更高版本支持给定的格式的驱动程序失败 set 格式请求为该格式，则可能会降低性能。 只有您能保证支持列表格式。

2.  驱动程序应允许在 pin 中 KSSTATE 上设置的媒体类型\_停止/KSSTATE\_运行。 不需要执行操作此处以外来确保该驱动程序不会不禁止这。

3.  该驱动程序应提供 intersect 处理程序中的[ **KSPIN\_描述符\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)。**IntersectHandler**对于每个插针。

4.  微型驱动程序应提供一个处理程序[ **KSPROPERTY\_连接\_PROPOSEDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-connection-proposedataformat)属性。

5.  如果设置的输出媒体类型，编码器应报告 （通过使用 pin 描述符） 可能输入的类型根据指定的输出媒体类型。 如果未设置输出媒体类型，则编码器应报告任何输入的媒体类型。

6.  如果输入的媒体类型设置，解码器应报告根据指定的输入的媒体类型的可能的输出类型。

7.  如果输入的媒体类型设置，视频处理器应报告根据指定的输入的媒体类型及其输出类型。

8.  该驱动程序应支持[ICodecAPI](https://docs.microsoft.com/en-us/previous-versions/ms784893(v%3Dvs.85))接口。 用户模式组件也可以通过使用此用户模式接口获得编解码器的配置信息。

9.  安装过程中的编码器，首先 ICodecAPI 设置的属性后, 跟输出媒体类型。 接着，编码器应仅使用当前配置中提供它可以支持的输入的类型。

10. **ICodecAPI**属性和编解码器 API 介质类型属性重叠在某些方面，例如，配置文件和级别。 在这些情况下，与媒体类型相关的编解码器 API 属性重写 ICodecAPI 属性。 设置媒体类型后，微型驱动程序不应允许修改这些重叠的属性。

11. 安装过程中的解码器，是首次设置输入的类型。 接着，解码器应提供仅输出类型，它可以支持使用其当前的输入类型。

12. 编码器的预期的输入应为 4:2:0，并且至少隔行扫描的 NV12 渐进/式。 预期的输出是一个压缩的基本流格式 MPEG2 PS / TS 或 H.264 附录 b。

13. 解码器的预期的输入是针对基本流。 预期的输出是未压缩 NV12 作为源流的不成比例的版本。

14. 插针上 AVStream 驱动程序应具有都相互独立的状态。 这意味着可以从转换输入插针**KSSTATE\_停止**达**KSSTATE\_运行**在输出插针保持**KSSTATE\_停止**状态。

15. 当微型驱动程序收到的 GET 请求属性，变量的数据缓冲区大小时，微型驱动程序应如何解释**NULL**作为查询的所需的缓冲区大小的缓冲区。 在这种情况下，该驱动程序应指定所需的长度的 Irp-&gt;IoStatus.Information 字段并返回状态\_缓冲区\_溢出。 此外，微型驱动程序应设置为警告而不是错误的返回代码。 例如，请按照本指南使用数据交集处理程序。
