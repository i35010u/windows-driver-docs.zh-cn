---
title: USB 音频 2.0 驱动程序
description: 从 Windows 10 版本 1703年，USB 音频 2.0 驱动程序随 Windows。 此驱动程序提供基本功能。
ms.date: 10/23/2018
ms.localizationpriority: medium
ms.openlocfilehash: fcdf5f1a141a94257ded52be6616ba068164912f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335387"
---
# <a name="usb-audio-20-drivers"></a>USB 音频 2.0 驱动程序

从 Windows 10 版本 1703年，USB 音频 2.0 驱动程序随 Windows。 它旨在支持 USB 音频 2.0 设备类。 WaveRT 音频端口类微型端口驱动程序。 有关 USB 音频 2.0 设备类的详细信息，请参阅[ https://www.usb.org/developers/docs/devclass_docs/ ](https://www.usb.org/developers/docs/devclass_docs/)。 

该驱动程序名为： _usbaudio2.sys_以及关联的 inf 文件是否_usbaudio2.inf_。

该驱动程序会在设备管理器中标识为"USB 音频类 2 设备"。 将覆盖 USB 产品字符串，该名称是否可用。

兼容设备附加到系统时，会自动启用该驱动程序。 但是，如果第三方驱动程序存在的系统或 Windows 更新，则该驱动程序将安装，并且重写类驱动程序。 

 
## <a name="architecture"></a>体系结构

USBAudio.Sys 适合更广泛的 Windows USB 音频体系结构所示。 

![在顶部和底部的 USB 音频设备显示 Kmixer.sys 堆栈关系图](images/usb-2-0-audio-arch.png)

## <a name="related-usb-specifications"></a>相关的 USB 规范

以下的 USB 规范定义 USB 音频和本主题中引用。

-   USB 2 是指通用串行总线规范，修订版本 2.0
-   ADC 2 是指 USB 设备类定义的音频设备，版本 2.0。
-   FMT 2 是指 2.0 版中的音频数据格式规范。

U-如果是特别兴趣组维护[官方 USB 规范](https://www.usb.org/developers/docs/)，测试规范和工具。 


## <a name="audio-formats"></a>音频格式
该驱动程序支持下面列出的格式。 一项备用设置以指定另一个 FMT 2 或未知的格式中定义的格式将被忽略。

我格式 (FMT 2 2.3.1) 的类型：
-   与每个样本的 8..32 位 PCM 格式 (FMT20 2.3.1.7.1)
-   PCM8 Format (FMT-2 2.3.1.7.2)
-   IEEE_FLOAT 格式 (FMT 2 2.3.1.7.3)

键入 III 格式 （FMT 2 2.3.3 和 A.2.3）：
-   IEC61937_AC-3
-   IEC61937_MPEG-2_AAC_ADTS
-   IEC61937_DTS-I
-   IEC61937_DTS-II
-   IEC61937_DTS-III
-   TYPE_III_WMA


## <a name="feature-descriptions"></a>功能描述

本部分介绍的功能的 USB 音频 2.0 驱动程序。 

### <a name="audio-function-topology"></a>音频函数拓扑

该驱动程序支持在 ADC 2 3.13 中定义的所有实体类型。

每个终端实体必须具有有效时钟连接兼容的 USB 音频 2.0 硬件中。 时钟路径可以根据需要包含时钟乘数和时钟选择器单位，时钟源实体结尾。

该驱动程序支持一个单一的时钟源。 如果设备实现多个时钟源实体和时钟选择器，该驱动程序将使用默认处于选中状态的时钟源，并将不会修改时钟选择器的位置。

不支持处理单元 (ADC 2 3.13.9) 与多个输入插针。

不支持使用多个输入插针一个扩展单元 (ADC 2 3.13.10)。

不允许在拓扑中的循环路径。


### <a name="audio-streaming"></a>音频流

该驱动程序支持以下终结点同步类型 (USB 2 5.12.4.1):

 -  异步 IN 和 OUT
 -  同步 IN 和 OUT
 -  自适应 IN 和 OUT

异步扩展用例的驱动程序支持显式的反馈。 必须在各自的备用设置 AS 接口的实现反馈终结点。 该驱动程序不支持隐式的反馈。

没有适用于设备的多个终结点使用共享的时钟的当前限制的支持。 

为自适应在用例驱动程序不支持前馈终结点。 如果备用设置中存在这样的终结点，则将忽略它。 驱动程序处理自适应在流中异步流的方式相同。

等时创建的设备的数据包的大小，必须在 FMT 2.0 部分 2.3.1.1 中指定的限制范围内。 这意味着快/慢一个音频槽不能超过正常大小从实际数据包大小的偏差 (音频槽 = 通道计数示例)。


## <a name="descriptors"></a>描述符

音频函数必须实现一个 AudioControl 接口描述符 (ADC 2 4.7) 和一个或多个 AudioStreaming 接口描述符 (ADC 2 4.9)。 不支持具有音频控件接口，但没有流式处理接口的函数。

该驱动程序支持 ADC20，第 4 节中定义的所有描述符类型。 以下各小节提供某些特定的描述符类型注释。

### <a name="class-specific-as-interface-descriptor"></a>特定于类的 AS 接口描述符 

有关此规范的详细信息，请参阅 ADC 2 4.9.2。

AS 接口描述符必须替代设置零且没有终结点 （即没有带宽消耗） 开头，必须进一步按升序排序兼容 USB 音频 2.0 硬件中的指定备用设置。

将忽略具有驱动程序不支持的格式的备用设置。

同步数据的终结点，并根据需要反馈终结点，必须指定每个非零值替代设置。 不支持不带任何终结点的非零值替代设置。

BTerminalLink 字段必须引用在拓扑中的终端实体和其值必须为 AS 接口的所有替代设置的相同。

中的 AS 接口描述符的 bFormatType 字段必须与相同 bFormatType 格式类型说明符 (FMT 2 2.3.1.6) 中指定。

对于 I 类型格式，完全有一位必须设置为其中一个 AS 接口描述符的 bmFormats 字段中。 否则，该驱动程序将忽略格式。

若要保存总线带宽，AS 接口可以同步数据终结点描述符中实现多个具有相同的格式 （根据 bNrChannels 和 AS 格式类型说明符） 但不同 wMaxPacketSize 值的替代设置。 对于给定的示例速率驱动程序会选择可以满足数据速率要求最小 wMaxPacketSize 的备用设置。

### <a name="type-i-format-type-descriptor"></a>设置类型描述符的格式类型

有关此规范的详细信息，请参阅 FMT 2 2.3.1.6。

以下限制适用：

|                            |                        |                               |
|----------------------------|------------------------|-------------------------------|
| 我键入 PCM 格式：         | 1 <= bSubslotSize <= 4 |     8 < = bBitResolution < = 32 |
| 我键入 PCM8 格式：        | bSubslotSize = = 1      |     bBitResolution = = 8       |
| 我键入 IEEE_FLOAT 格式：  | bSubslotSize = = 4      |     bBitResolution = = 32      | 
| 键入 III IEC61937 格式： | bSubslotSize = = 2      |     bBitResolution = = 16      |


### <a name="class-specific-as-isochronous-audio-data-endpoint-descriptor"></a>特定于类的 AS 同步的音频数据终结点描述符 

有关此规范的详细信息，请参阅 ADC 2 4.10.1.2。

BmAttributes 字段中的 MaxPacketsOnly 标志不受支持，并将被忽略。

字段 bmControls、 bLockDelayUnits 和 wLockDelay 将被忽略。


## <a name="class-requests-and-interrupt-data-messages"></a>类请求和中断数据消息

该驱动程序支持在 ADC-2，第 5.2 节中定义的控件请求的子集和支持的某些控件中断数据消息 (ADC 2 6.1)。 下表显示了驱动程序中实现的子集。

| 实体           | 控件                    | 获取当前 | 集 CUR | 获取范围 | 中断 |
|------------------|----------------------------|---------|---------|-----------|-----------|
| 时钟源     | 采样频率控件 | x       | x       | x         |           |
| 时钟选择器   | 时钟选择器控件     | x       |         |           |           |
| 时钟乘数 | 分子控件          | x       |         |           |           |
|                  | 分母控件        | x       |         |           |           |
| 终端         | 连接器控件          | x       |         |           | x         |
| Mixer 单元       | Mixer 控件              | x       | x       | x         |           |
| 选择器单元    | 选择器控件           | x       | x       |           |           |
| 功能单元     | 静音控件               | x       | x       |           | x         |
|                  | 音量控制             | x       | x       | x         | x         |
|                  | 自动增益控制     | x       | x       |           |           |
| 影响单元      | –                          |         |         |           |           |
| 处理单元  | –                          |         |         |           |           |
| 扩展单元   | –                          |         |         |           |           |


在以下各部分提供了有关控件和请求的其他信息。

### <a name="clock-source-entity"></a>时钟源实体 

有关此规范的详细信息，请参阅 ADC 2 5.2.5.1。

至少，时钟源实体必须兼容的 USB 音频 2.0 硬件中实现采样频率控件获取范围和获取当前请求 (ADC 2 5.2.5.1.1)。

采样频率控件获取范围请求将返回一系列子范围 (ADC 2 5.2.1 章)。 每个子范围描述离散的频率或频率范围。 必须通过将最小值和最大字段设置为各自的频率和 RES 为零表示离散的采样频率。 各个子范围不能重叠。 如果子范围重叠前一个，该驱动程序将忽略它。

这将实现一个单一的固定的频率时钟源实体仅不需要实现采样频率控件设置 CUR。 它实现了获取 CUR 返回固定的频率，并实现获取范围将报告一个单一的离散频率。

### <a name="clock-selector-entity"></a>时钟选择器实体 

有关此规范的详细信息，请参阅 ADC 2 5.2.5.2

USB 音频 2.0 驱动程序不支持时钟选择。 驱动程序使用时钟源实体，它默认处于选中状态并永远不会发出一个时钟选择器控件设置当前请求。 时钟选择器控件获取当前请求 (ADC 2 5.2.5.2.1) 必须兼容的 USB 音频 2.0 硬件中实现。 


### <a name="feature-unit"></a>功能单元 

有关此规范的详细信息，请参阅 ADC 2 5.2.5.7。

该驱动程序支持一个单个卷范围。 如果卷控件获取范围请求返回多个范围，则将忽略后续的范围。

最小值和最大字段所表达的卷间隔应为整数指定 RES 字段中的步大小的倍数。

如果一项功能实现为静音或卷单通道控件，以及主控件，该驱动程序使用单通道控件，并忽略大纲控件。



## <a name="additional-information-for-oem-and-ihvs"></a>OEM 和 Ihv 的其他信息

Oem 和 Ihv 应测试提供的现成驱动程序对其现有的和新设备。

没有任何特定的合作伙伴自定义项与现成 USB 音频 2.0 驱动程序相关联。

（在更新中提供给 Windows 版本 1703年） 此 INF 文件条目，用于识别现成驱动程序是一个通用设备驱动程序。 

```inf
GenericDriverInstalled,,,,1
```


为以下兼容 Id 与 usbaudio2.inf 注册现成驱动程序。

```inf
USB\Class_01&SubClass_00&Prot_20
USB\Class_01&SubClass_01&Prot_20
USB\Class_01&SubClass_02&Prot_20
USB\Class_01&SubClass_03&Prot_20
```

请参阅子类类型 USB 音频 2.0 规范。

与 MIDI （子类 0x03 更高版本） 的 USB 音频 2.0 设备将枚举加载的 MIDI 函数作为具有 usbaudio.sys （USB 音频 1.0 驱动程序） 的单独多功能设备。 

USB 音频 1.0 类驱动程序使用 wdma_usb.inf 注册此兼容 ID。
 
```inf
USB\Class_01
```
 
因此，具有这些排除项：
 
```inf
USB\Class_01&SubClass_00&Prot_20
USB\Class_01&SubClass_01&Prot_20
USB\Class_01&SubClass_02&Prot_20
USB\Class_01&SubClass_03&Prot_20
```

由于 Windows 音频堆栈的限制的共享模式中不支持任意数量的通道 （大于 8）。


## <a name="ihv-usb-audio-20-drivers-and-updates"></a>IHV USB 音频 2.0 驱动程序和更新
有关 IHV 提供第三方驱动程序 USB 音频 2.0 驱动程序，这些驱动程序将继续其设备的首选我们现成驱动程序通过除非他们更新其驱动程序以显式重写此行为并使用现成驱动程序。 

## <a name="audio-jack-registry-descriptions"></a>音频插孔注册表说明

启动 Windows 10 版本 1703，Ihv 创建 USB 音频类 2.0 中一个或多个插座的设备不来描述这些插孔内置音频类 2.0 驱动程序的功能。 在处理此设备 KSPROPERTY_JACK_DESCRIPTION，现成驱动程序将使用提供的 jack 信息。

Jack 信息存储在注册表中的设备实例密钥 （HW 密钥）。

下面介绍在注册表中的音频插孔信息设置：

```text
REG_DWORD  T<tid>_NrJacks                 # of the jack on this device
REG_DWORD  T<tid>_J<n>_ChannelMapping     Channel mask. The value is defined in ksmedia.h. e.g. SPEAKER_FRONT_RIGHT or KSAUDIO_SPEAKER_5POINT1_SURROUND
REG_DWORD  T<tid>_J<n>_ConnectorType      The enum value is define in EPcxConnectionType. 
REG_DWORD  T<tid>_J<n>_GeoLocation        The enum value is define in EPcxGeoLocation.
REG_DWORD  T<tid>_J<n>_GenLocation        The enum value is define in EPcxGenLocation.
REG_DWORD  T<tid>_J<n>_PortConnection     The enum value is define in EPxcPortConnection.
REG_DWORD  T<tid>_J<n>_Color              The color needs to be represent by RGB like this: 0x00RRGGBB (NOT a COLORREF).
```

\<tid\> = 终端 ID （如描述符中定义）
  
\<n\> = Jack 数 (1 ~ n)。 

约定\<tid\>并\<n\>是：

- Base 10 (8、 9、 10 而不是 8、 9)
- 没有前导零
- n 是从 1 开始 （第一个是 jack 是 jack 1，而非 jack 0）

例如： 

T1_NrJacks, T1_J2_ChannelMapping, T1_J2_ConnectorType

有关更多的音频插孔的信息，请参阅[KSJACK_DESCRIPTION 结构](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)。

可以以各种方式设置这些注册表值： 

- 使用自定义 Inf 的包装为目的现成 INF，来设置这些值。

- 直接通过 USB 设备 （请参阅下面的示例） 的硬件设备通过 Microsoft OS 描述符。 有关创建这些描述符的详细信息，请参阅[USB 设备的 Microsoft 操作系统描述符](https://docs.microsoft.com/windows-hardware/drivers/usbcon/microsoft-defined-usb-descriptors)。

### <a name="microsoft-os-descriptors-for-usb-example"></a>Microsoft 操作系统描述符的 USB 示例

USB 示例以下 Microsoft OS 描述符包含的通道映射和一个 jack 的颜色。 示例适用于具有单个功能描述符的非复合设备。 

IHV 供应商应扩展它以包含有关 jack 说明的任何其他信息。 


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


## <a name="troubleshooting"></a>疑难解答
如果该驱动程序未启动，应检查系统事件日志。 该驱动程序记录指示故障的原因的事件。 同样，音频可以手动收集日志中所述的步骤[此博客文章](https://blogs.msdn.microsoft.com/matthew_van_eerde/2017/01/09/collecting-audio-logs-the-old-fashioned-way/)。 如果失败可能表示驱动程序问题，请报告它使用，如下所述的反馈中心，并包括日志。

有关如何为 USB 音频 2.0 类驱动程序使用补充 TMF 文件中读取日志的信息，请参阅[此博客文章](https://blogs.msdn.microsoft.com/matthew_van_eerde/2017/10/23/how-to-gather-and-read-logs-for-microsofts-usb-audio-2-0-class-driver/)。 有关使用 TMF 文件的常规信息，请参阅[显示包含 TMF 文件的跟踪日志](https://docs.microsoft.com/windows-hardware/drivers/devtest/displaying-a-trace-log-with-a-tmf-file)。

## <a name="feedback-hub"></a>反馈中心
如果遇到此驱动程序问题，请收集音频日志，然后按照中所述步骤[此博客文章](https://blogs.msdn.microsoft.com/matthew_van_eerde/2016/09/26/report-problems-with-logs-and-suggest-features-with-the-feedback-hub/)以使其通过反馈中心我们注意到。


## <a name="driver-development"></a>驱动程序开发 

此 USB 音频 2.0 类驱动程序由 Thesycon 开发，Microsoft 支持。


### <a name="see-also"></a>请参阅

[Windows Driver Model (WDM)](https://msdn.microsoft.com/library/windows/hardware/ff565698)

[音频驱动程序概述](https://docs.microsoft.com/windows-hardware/drivers/audio/getting-started-with-wdm-audio-drivers)

[WaveRT 端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/audio/introducing-the-wavert-port-driver)

[低滞后时间的音频](https://docs.microsoft.com/windows-hardware/drivers/audio/low-latency-audio)




