---
title: USB 音频 2.0 驱动程序
description: 从 Windows 10 开始，版本1703，Windows 附带了一个 USB 音频2.0 驱动程序。 此驱动程序提供基本功能。
ms.date: 12/19/2019
ms.localizationpriority: medium
ms.topic: article
ms.custom:
- CI 111498
- CSSTroubleshooting
ms.openlocfilehash: a8989f52c9b5f6b4223c6c5ee60bac692df97474
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606383"
---
# <a name="usb-audio-20-drivers"></a>USB 音频 2.0 驱动程序

从 Windows 10 开始，版本1703，Windows 附带了一个 USB 音频2.0 驱动程序。 它设计为支持 USB 音频2.0 设备类。 驱动程序是 WaveRT 的音频端口类微型端口。 有关 USB 音频2.0 设备类的详细信息，请参阅[https://www.usb.org/documents?search=&type%5B0%5D=55&items_per_page=50](https://www.usb.org/documents?search=&type%5B0%5D=55&items_per_page=50)。

该驱动程序名为： _usbaudio2_ ，关联的 inf 文件为_usbaudio2_。

驱动程序将在设备管理器中标识为 "USB 音频类2设备"。 如果该名称可用，将使用 USB 产品字符串覆盖此名称。

当兼容设备连接到系统时，会自动启用该驱动程序。 但是，如果系统或 Windows 更新上存在第三方驱动程序，则将安装该驱动程序并替代类驱动程序。

## <a name="architecture"></a>体系结构

USBAudio 适用于 Windows USB 音频的更广泛的体系结构，如下所示。 

![在顶部显示 Kmixer 的堆栈关系图，底部显示一个 USB 音频设备](images/usb-2-0-audio-arch.png)

## <a name="related-usb-specifications"></a>相关 USB 规范

以下 USB 规范定义 USB 音频，在本主题中进行了引用。

- USB-2 指通用串行总线规范，版本2。0
- ADC-2 指音频设备的 USB 设备类定义，版本2.0。
- BCP.FMT-2 指音频数据格式规范，版本2.0。

USB-如果是一个特殊的兴趣组，其中维护了[官方 USB 规范](https://www.usb.org/documents)、测试规范和工具。

## <a name="audio-formats"></a>音频格式

驱动程序支持下面列出的格式。 将忽略另一个设置，该设置指定 BCP.FMT 中定义的另一种格式（或未知格式）。

键入 I 格式（BCP.FMT）：

- 每个样本有8个32位的 PCM 格式（FMT20 2.3.1.7.1）
- PCM8 格式（BCP.FMT-2 2.3.1.7.2）
- IEEE_FLOAT 格式（BCP.FMT-2 2.3.1.7.3）

类型 III 格式（BCP.FMT-2 2.3.3 和2.3）：

- IEC61937_AC-3
- IEC61937_MPEG-2_AAC_ADTS
- IEC61937_DTS-I
- IEC61937_DTS II
- IEC61937_DTS-III
- TYPE_III_WMA

## <a name="feature-descriptions"></a>功能描述

本部分介绍 USB 音频2.0 驱动程序的功能。

### <a name="audio-function-topology"></a>音频函数拓扑

该驱动程序支持在 ADC-2 3.13 中定义的所有实体类型。

每个终端实体都必须具有一个兼容 USB 音频2.0 硬件的有效时钟连接。 时钟路径可以有选择性地包含时钟乘数和时钟选择器单位，并且必须以时钟源实体结束。

驱动程序仅支持一个时钟源。 如果设备实现了多个时钟源实体和一个时钟选择器，则驱动程序将使用默认情况下选择的时钟源，而不会修改时钟选择器的位置。

不支持具有多个输入 pin 的处理单元（ADC-2 3.13.9）。

不支持具有多个输入 pin 的扩展单元（ADC-2 3.13.10）。

不允许拓扑中的循环路径。

### <a name="audio-streaming"></a>音频流式处理

驱动程序支持以下终结点同步类型（USB-2 5.12.4.1）：

- 异步入和移出
- 同步进出
- 自适应放大和缩小

对于异步 OUT 事例，驱动程序仅支持显式反馈。 必须在作为接口的各自备用设置中实现反馈终结点。 该驱动程序不支持隐式反馈。

对于使用多个终结点的共享时钟的设备，目前有有限的支持。 

如果驱动程序不支持 feedforward 终结点，则为。 如果该终结点存在于备用设置中，则将被忽略。 驱动程序以与异步 IN stream 相同的方式处理流式处理中的自适应。

设备创建的同步数据包大小必须在 BCP.FMT-2.0 部分2.3.1.1 中指定的限制范围内。 这意味着实际数据包大小与名义大小的偏差不能超过 +/-一个音频槽（音频槽 = 通道计数样本）。

## <a name="descriptors"></a>描述符

音频函数必须仅实现一个 AudioControl 接口描述符（ADC-2 4.7）以及一个或多个 AudioStreaming 接口描述符（ADC-2 4.9）。 具有音频控制接口但不支持流接口的函数。

该驱动程序支持 ADC20 中定义的所有描述符类型，第4部分。 以下各部分提供了有关某些特定描述符类型的注释。

### <a name="class-specific-as-interface-descriptor"></a>类特定为接口描述符

有关此规范的详细信息，请参阅 ADC-2 4.9.2。

AS 接口描述符必须以无终结点（无带宽消耗）的备用设置0开始，并且必须在兼容 USB 音频2.0 硬件中按升序指定进一步的备用设置。

不受驱动程序支持的格式的备用设置将被忽略。

每个非零的备用设置都必须指定一个同步数据终结点，还可以有一个反馈终结点。 不支持不含任何终结点的非零备用设置。

BTerminalLink 字段必须引用拓扑中的终端实体，并且它的值必须与 AS 接口的所有备用设置相同。

AS 接口描述符中的 bFormatType 字段必须与在格式类型描述符（BCP.FMT-2 2.3.1.6）中指定的 bFormatType 相同。

对于类型 I 格式，必须在 AS 接口描述符的 bmFormats 字段中设置一个位。 否则，驱动程序将忽略格式。

为了节省总线带宽，一个接口可以实现具有相同格式的多个备用设置（在 bNrChannels 和 AS 格式类型描述符中），但在同步数据终结点描述符中具有不同的 wMaxPacketSize 值。 对于给定的采样率，驱动程序将选择具有可满足数据速率要求的最小 wMaxPacketSize 的备用设置。

### <a name="type-i-format-type-descriptor"></a>键入 I 格式类型描述符

有关此规范的详细信息，请参阅 BCP.FMT-2 2.3.1.6。

存在以下限制：

|                            |                        |                               |
|----------------------------|------------------------|-------------------------------|
| 键入 I PCM 格式：         | 1 < = bSubslotSize < = 4 |     8 < = bBitResolution < = 32 |
| 键入 I PCM8 format：        | bSubslotSize = = 1      |     bBitResolution = = 8       |
| 键入我 IEEE_FLOAT 的格式：  | bSubslotSize = = 4      |     bBitResolution = = 32      |
| 类型 III IEC61937 格式： | bSubslotSize = = 2      |     bBitResolution = = 16      |

### <a name="class-specific-as-isochronous-audio-data-endpoint-descriptor"></a>类特定于同步音频数据终结点描述符 

有关此规范的详细信息，请参阅 ADC-2 4.10.1.2。

"BmAttributes" 字段中的 MaxPacketsOnly 标志不受支持，将被忽略。

将忽略字段 bmControls、bLockDelayUnits 和 wLockDelay。

## <a name="class-requests-and-interrupt-data-messages"></a>类请求和中断数据消息

该驱动程序支持在 ADC-2、5.2 节中定义的控制请求的一个子集，并支持某些控件的中断数据消息（ADC-2 6.1）。 下表显示了驱动程序中实现的子集。

| 实体           | 控件                    | 获取当前 | 设置当前 | 获取范围 | 妨碍 |
|------------------|----------------------------|---------|---------|-----------|-----------|
| 时钟源     | 采样频率控制 | x       | x       | x         |           |
| 时钟选择器   | 时钟选择器控件     | x       |         |           |           |
| 时钟乘数 | 分子控件          | x       |         |           |           |
|                  | 分母控件        | x       |         |           |           |
| 终端         | 连接器控件          | x       |         |           | x         |
| 混音器单位       | 混音器控制              | x       | x       | x         |           |
| 选择器单位    | 选择器控件           | x       | x       |           |           |
| 功能单元     | 静音控件               | x       | x       |           | x         |
|                  | 音量控制             | x       | x       | x         | x         |
|                  | 自动增益控制     | x       | x       |           |           |
| 效果单位      | –                          |         |         |           |           |
| 处理单元  | –                          |         |         |           |           |
| 扩展单元   | –                          |         |         |           |           |

以下子节提供了有关控件和请求的其他信息。

### <a name="clock-source-entity"></a>时钟源实体

有关此规范的详细信息，请参阅 ADC-2 5.2.5.1。

时钟源实体至少必须在兼容的 USB 音频2.0 硬件中实现采样频率控制获取范围并获取当前请求（ADC-2 5.2.5.1.1）。

采样频率控制获取范围请求返回子范围（ADC-2 5.2.1）的列表。 每个子范围描述离散的频率或频率范围。 必须通过将最小和最大字段设置为相应的频率，将 RES 设置为零，来表示离散的采样频率。 单个子范围不能重叠。 如果子范围与上一个子范围重叠，则驱动程序将忽略它。

仅实现一个固定频率的时钟源实体无需实现采样频率控制集。 它实现了 "获取"，它将返回固定的频率，并实现报告单一离散频率的 "获取范围"。

### <a name="clock-selector-entity"></a>时钟选择器实体

有关此规范的详细信息，请参阅 ADC-2 5.2.5。2

USB 音频2.0 驱动程序不支持时钟选择。 该驱动程序使用默认情况下选择的 "时钟源" 实体，并且决不会发出时钟选择器控制集的当前请求。 时钟选择器控件获取当前请求（ADC-2 5.2.5.2.1）必须在兼容的 USB 音频2.0 硬件中实现。

### <a name="feature-unit"></a>功能单元

有关此规范的详细信息，请参阅 ADC-2 5.2.5.7。

驱动程序仅支持一个卷范围。 如果卷控制获取范围请求返回多个范围，则将忽略后续范围。

最小和最大字段表示的卷间隔应为 RES 字段中指定的步长大小的整数倍。

如果某个功能单元实现了单通道控件以及静音或音量的主控件，则驱动程序将使用单个通道控件并忽略主控件。

## <a name="additional-information-for-oem-and-ihvs"></a>有关 OEM 和 Ihv 的其他信息

Oem 和 Ihv 应根据提供的内置驱动程序来测试其现有的和新的设备。

没有与内置 USB 音频2.0 驱动程序关联的特定合作伙伴自定义。

此 INF 文件条目（在 Windows 版本1703的更新中提供）用于标识内置驱动程序为通用设备驱动程序。

```inf
GenericDriverInstalled,,,,1
```

内置驱动程序向 usbaudio2 注册以下兼容 Id。

```inf
USB\Class_01&SubClass_00&Prot_20
USB\Class_01&SubClass_01&Prot_20
USB\Class_01&SubClass_02&Prot_20
USB\Class_01&SubClass_03&Prot_20
```

请参阅适用于子类类型的 USB 音频2.0 规范。

带 MIDI （上面的子类0x03）的 USB 音频2.0 设备将使用已加载 usbaudio （USB 音频1.0 驱动程序）的独立多功能设备枚举 MIDI 函数。

USB 音频1.0 类驱动程序将此兼容 ID 注册到 wdma_usb。

```inf
USB\Class_01
```

并且具有以下排除项：

```inf
USB\Class_01&SubClass_00&Prot_20
USB\Class_01&SubClass_01&Prot_20
USB\Class_01&SubClass_02&Prot_20
USB\Class_01&SubClass_03&Prot_20
```

由于 Windows 音频堆栈的限制，在共享模式下不支持任意数量的通道（超过8个）。

## <a name="ihv-usb-audio-20-drivers-and-updates"></a>IHV USB 音频2.0 驱动程序和更新

对于 IHV 提供的第三方驱动程序 USB 音频2.0 驱动程序，这些驱动程序将继续在其内置驱动程序的设备上首选，除非它们更新其驱动程序以显式覆盖此行为并使用内置驱动程序。 

## <a name="audio-jack-registry-descriptions"></a>音频插孔注册表说明

从 Windows 10 版本1703开始，创建具有一个或多个插座的 USB 音频类2.0 设备的 Ihv 能够将这些插孔描述为内置音频类2.0 驱动程序。 当处理此设备的 KSPROPERTY_JACK_DESCRIPTION 时，内置驱动程序使用提供的插座信息。

插座信息存储在设备实例密钥（HW 密钥）的注册表中。

下面描述了注册表中的音频插孔信息设置：

```text
REG_DWORD  T<tid>_NrJacks                 # of the jack on this device
REG_DWORD  T<tid>_J<n>_ChannelMapping     Channel mask. The value is defined in ksmedia.h. e.g. SPEAKER_FRONT_RIGHT or KSAUDIO_SPEAKER_5POINT1_SURROUND
REG_DWORD  T<tid>_J<n>_ConnectorType      The enum value is define in EPcxConnectionType. 
REG_DWORD  T<tid>_J<n>_GeoLocation        The enum value is define in EPcxGeoLocation.
REG_DWORD  T<tid>_J<n>_GenLocation        The enum value is define in EPcxGenLocation.
REG_DWORD  T<tid>_J<n>_PortConnection     The enum value is define in EPxcPortConnection.
REG_DWORD  T<tid>_J<n>_Color              The color needs to be represent by RGB like this: 0x00RRGGBB (NOT a COLORREF).
```

\<tid\> = 终端 ID （在描述符中定义）
  
\<n\> = 插孔号（1 ~ n）。 

\<tid\> 和 \<n 的约定\> 为：

- 基数为10（8，9，10，而不是8，9，a）
- 无前导零
- n 从1开始（第一个插孔是插孔1而不是插孔0）

例如：

T1_NrJacks、T1_J2_ChannelMapping T1_J2_ConnectorType

有关音频插孔的其他信息，请参阅[KSJACK_DESCRIPTION 结构](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)。

可以通过多种方式设置这些注册表值：

- 使用自定义 Inf 来包装内置 INF，以设置这些值。

- 通过 USB 设备的 Microsoft OS 描述符直接通过 "h/w" 设备（请参阅下面的示例）。 有关创建这些描述符的详细信息，请参阅[MICROSOFT OS 描述符 FOR USB 设备](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)。

### <a name="microsoft-os-descriptors-for-usb-example"></a>Microsoft OS 描述符 for USB 示例

以下适用于 USB 的 Microsoft OS 描述符示例包含一个插孔的通道映射和颜色。 此示例针对具有单个功能描述符的非复合设备。

IHV 供应商应该将其扩展为包含插孔说明的任何其他信息。

```text
UCHAR Example2_MSOS20DescriptorSetForUAC2 [0x76] = {
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,             // wLength - 10 bytes
    0x00, 0x00,             // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06, // dwWindowsVersion – 0x060?0000 for future Windows version
    0x76, 0x00,             // wTotalLength – 118 bytes // update later

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x42, 0x00,             // bLength - 66 bytes
    0x04, 0x00,             // wDescriptorType – 5 for Registry Property
    0x04, 0x00,             // wPropertyDataType - 4 for REG_DWORD
    0x34, 0x00,             // wPropertyNameLength – 52 bytes
    0x54, 0x00, 0x30, 0x00, // Property Name - “T01_J01_ChannelMapping”
    0x31, 0x00, 0x5f, 0x00,
    0x4a, 0x00, 0x30, 0x00,
    0x31, 0x00, 0x5f, 0x00,
    0x43, 0x00, 0x68, 0x00,
    0x61, 0x00, 0x6e, 0x00,
    0x6e, 0x00, 0x65, 0x00,
    0x6c, 0x00, 0x4d, 0x00,
    0x61, 0x00, 0x70, 0x00,
    0x70, 0x00, 0x69, 0x00,
    0x6e, 0x00, 0x67, 0x00,
    0x00, 0x00
    0x04, 0x00,                       // wPropertyDataLength – 4 bytes
    0x02, 0x00, 0x00, 0x00  // PropertyData - SPEAKER_FRONT_RIGHT

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x2A, 0x00,             // bLength - 42 bytes
    0x04, 0x00,             // wDescriptorType – 5 for Registry Property
    0x04, 0x00,             // wPropertyDataType - 4 for REG_DWORD
    0x1C, 0x00,             // wPropertyNameLength – 28 bytes
    0x54, 0x00, 0x30, 0x00, // Property Name - “T01_J01_Color”
    0x31, 0x00, 0x5f, 0x00,
    0x4a, 0x00, 0x30, 0x00,
    0x31, 0x00, 0x5f, 0x00,
    0x43, 0x00, 0x6f, 0x00,
    0x6c, 0x00, 0x6f, 0x00,
    0x72, 0x00, 0x00, 0x00,
    0x04, 0x00,             // wPropertyDataLength – 4 bytes
    0x00, 0x00, 0xff, 0x00  // PropertyData - 0xff0000 - RED }
```

## <a name="troubleshooting"></a>“疑难解答”

如果驱动程序未启动，则应检查系统事件日志。 驱动程序记录指示失败原因的事件。 同样，可以按照[此博客文章](https://matthewvaneerde.wordpress.com/2017/01/09/collecting-audio-logs-the-old-fashioned-way/)中所述的步骤手动收集音频日志。 如果失败可能表示驱动程序出现问题，请使用下面所述的反馈中心进行报告，并包含日志。

有关如何使用补充 TMF 文件读取 USB 音频2.0 类驱动程序的日志的信息，请参阅[此博客文章](https://matthewvaneerde.wordpress.com/2016/09/26/report-problems-with-logs-and-suggest-features-with-the-feedback-hub//)。 有关使用 TMF 文件的常规信息，请参阅[使用 TMF 文件显示跟踪日志](https://docs.microsoft.com/windows-hardware/drivers/devtest/displaying-a-trace-log-with-a-tmf-file)。

有关 "音频服务未响应" 错误和 USB 音频设备在 Windows 10 版本1703中不起作用的信息，请参阅[Usb 音频未播放](usb-audio-not-playing.md)

## <a name="feedback-hub"></a>反馈中心

如果遇到此驱动程序问题，请收集音频日志，然后按照[此博客文章](https://blogs.msdn.microsoft.com/matthew_van_eerde/2016/09/26/report-problems-with-logs-and-suggest-features-with-the-feedback-hub/)中所述的步骤操作，通过反馈中心来关注。

## <a name="driver-development"></a>驱动程序开发

此 USB 音频2.0 类驱动程序由 Thesycon 开发，由 Microsoft 支持。

### <a name="see-also"></a>另请参阅

[Windows 驱动模型（WDM）](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)

[音频驱动程序概述](https://docs.microsoft.com/windows-hardware/drivers/audio/getting-started-with-wdm-audio-drivers)

[WaveRT 端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/introducing-the-wavert-port-driver)

[低延迟音频](https://docs.microsoft.com/windows-hardware/drivers/audio/low-latency-audio)
