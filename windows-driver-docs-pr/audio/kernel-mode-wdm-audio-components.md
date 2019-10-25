---
title: 内核模式 WDM 音频组件
description: 内核模式 WDM 音频组件
ms.assetid: 827997e2-6f07-4635-ac35-4ad026b82eae
keywords:
- 内核模式组件 WDK 音频
- WDMAud 系统驱动程序 WDK 音频
- SysAudio 系统驱动程序 WDK 音频
- KMixer 系统驱动程序 WDK 音频
- Redbook 系统驱动程序 WDK 音频
- SBEmul 系统驱动程序 WDK 音频
- SWMidi 系统驱动程序 WDK 音频
- DMusic 系统驱动程序 WDK 音频
- AEC WDK 音频
- DRMK 系统驱动程序 WDK 音频
- 拆分系统驱动程序 WDK 音频
- 端口类适配器驱动程序 WDK 音频
- USBAudio 类系统驱动程序 WDK 音频
- AVCAudio 类系统驱动程序 WDK 音频
- 1394 WDK 音频
- KMixer 系统驱动程序 WDK 音频，关于 KMixer 系统驱动程序
- IEEE 1394 WDK 音频
- WDM 音频组件 WDK
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 85056150cd27c1d6c0f9246549c73a5bdd32e812
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833178"
---
# <a name="kernel-mode-wdm-audio-components"></a>内核模式 WDM 音频组件


## <span id="kernel_mode_wdm_audio_components"></span><span id="KERNEL_MODE_WDM_AUDIO_COMPONENTS"></span>


内核模式 Microsoft Windows 驱动模型（WDM）音频组件如下：

WDMAud 系统驱动程序

SysAudio 系统驱动程序

KMixer 系统驱动程序

Redbook 系统驱动程序

SBEmul 系统驱动程序

SWMidi 系统驱动程序

DMusic 系统驱动程序

AEC 系统驱动程序

DRMK 系统驱动程序

拆分系统驱动程序

端口类适配器驱动程序和 PortCls 系统驱动程序

USB 音频类系统驱动程序 (Usbaudio.sys)

AVCAudio 类系统驱动程序

### <a name="span-idkm_wdmaud_system_driverspanspan-idkm_wdmaud_system_driverspanwdmaud-system-driver"></a><span id="km_wdmaud_system_driver"></span><span id="KM_WDMAUD_SYSTEM_DRIVER"></span>WDMAud 系统驱动程序

内核模式 WDMAud 系统驱动程序（Wdmaud）与用户模式 WDMAud 系统驱动程序（Wdmaud. winspool.drv）配对。 在用户模式 Microsoft Windows 多媒体系统调用和内核流式处理 i/o 请求之间转换的 WDMAud 驱动程序对。 WDMAud 为以下 Api 执行 i/o： **waveIn**、 **waveOut**、 **midiIn**、 **midiOut**、**混音**器和**aux** （Microsoft Windows SDK 文档中所述）。 内核模式 WDMAud 驱动程序是内核流式处理（KS）筛选器和 SysAudio 系统驱动程序的客户端。

### <a name="span-idsysaudio_system_driverspanspan-idsysaudio_system_driverspansysaudio-system-driver"></a><span id="sysaudio_system_driver"></span><span id="SYSAUDIO_SYSTEM_DRIVER"></span>SysAudio 系统驱动程序

SysAudio 系统驱动程序（Sysaudio）生成用于呈现和捕获音频内容的筛选器图形。 SysAudio 驱动程序将音频筛选器图形表示为[虚拟音频设备](virtual-audio-devices.md)，并将每个虚拟音频设备注册为 KSCATEGORY\_音频\_设备设备接口的实例。 （适配器驱动程序不应在此类别中注册自身，这种情况下专门为 SysAudio 保留。）例如，虚拟 MIDI 设备可能代表通过连接 SWMidi 驱动程序、KMixer 驱动程序和端口/微型端口驱动程序创建的筛选器图。 客户端仅与虚拟音频设备通信，而不是与构成虚拟音频设备的单个设备通信。 SysAudio 驱动程序对于客户端是透明的，它在连接的筛选器图中配置所有 KS 筛选器，以形成虚拟音频设备。 以下音频流源使用 SysAudio 生成的关系图：

-   DirectSound （请参阅 Microsoft Windows SDK 文档。）

-   Windows 多媒体 Api **waveIn**、 **waveOut**、 **midiIn**、 **midiOut**、**混音**器和**aux** （请参阅 Windows SDK 文档。）

-   Redbook CD 数字音频（请参阅 Redbook 系统驱动程序。）

-   声霸卡模拟器（请参阅 SBEmul 系统驱动程序。）

-   内核模式软件合成程序（请参阅 SWMidi 系统驱动程序和 DMusic 系统驱动程序。）

-   DRMK 系统驱动程序

### <a name="span-idkmixer_system_driverspanspan-idkmixer_system_driverspankmixer-system-driver"></a><span id="kmixer_system_driver"></span><span id="KMIXER_SYSTEM_DRIVER"></span>KMixer 系统驱动程序

KMixer 系统驱动程序（Kmixer）是用于执行以下操作的 KS 筛选器：

-   混合多个 PCM 音频流

-   高质量格式转换

-   位深度转换

-   扬声器配置和通道映射

除了简单的8位和16位的 mono 和立体声数据格式，KMixer 驱动程序还支持：

-   PCM 和 IEEE 浮点数据

-   位深度大于16位，通道格式具有两个以上的通道

-   头相关传输函数（HRTF）三维处理

有关各个版本 Windows 中的卷范围和默认卷级别的信息，请参阅[默认音频音量设置](default-audio-volume-settings.md)。

### <a name="span-idredbook_system_driverspanspan-idredbook_system_driverspanredbook-system-driver"></a><span id="redbook_system_driver"></span><span id="REDBOOK_SYSTEM_DRIVER"></span>Redbook 系统驱动程序

Redbook 系统驱动程序（Redbook）是管理 CD 数字音频呈现的 KS 筛选器。 Redbook 驱动程序是 SysAudio 系统驱动程序的客户端。 系统通过文件系统将 CD 数字音频路由到 Redbook 驱动程序，然后路由到 SysAudio 驱动程序。 CD 数字音频呈现在首选波形输出设备上（在 "控制面板" 的 "多媒体" 属性页中设置）。

### <a name="span-idsbemul_system_driverspanspan-idsbemul_system_driverspansbemul-system-driver"></a><span id="sbemul_system_driver"></span><span id="SBEMUL_SYSTEM_DRIVER"></span>SBEmul 系统驱动程序

SBEmul 系统驱动程序（Sbemul）为 MS-DOS 应用程序提供声霸卡声。 SBEmul 驱动程序是 SysAudio 系统驱动程序的客户端。 为了呈现和捕获内容，SysAudio 驱动程序使用首选的 wave 和 MIDI 设备（在 "控制面板" 的多媒体属性页中设置）。

只有 Windows 98/Me 支持声霸卡模拟。

### <a name="span-idswmidi_system_driverspanspan-idswmidi_system_driverspanswmidi-system-driver"></a><span id="swmidi_system_driver"></span><span id="SWMIDI_SYSTEM_DRIVER"></span>SWMidi 系统驱动程序

SWMidi 系统驱动程序（Swmidi）是一个 KS 筛选器，它提供软件模拟的通用 MIDI （GM）和高质量 Roland GS wavetable 合成。 如果硬件合成器不可用，则 **midiOut * * Xxx*应用程序将使用 SWMidi。 SWMidi 筛选器接收来自 WDMAud 系统驱动程序的带有时间戳的 MIDI 流的输入，并将 PCM 波纹流输出到 KMixer 系统驱动程序。 SWMidi 在内部混合其所有声音，形成一个带有 PCM 波纹格式的双通道输出流。

### <a name="span-iddmusic_system_driverspanspan-iddmusic_system_driverspandmusic-system-driver"></a><span id="dmusic_system_driver"></span><span id="DMUSIC_SYSTEM_DRIVER"></span>DMusic 系统驱动程序

DMusic 系统驱动程序（Dmusic）是一个 KS 筛选器，支持软件仿真、高质量、可下载的声音（DLS）合成。 DMusic 驱动程序是系统提供的端口类微型端口驱动程序。 它公开了支持[DirectMusic 流数据范围](directmusic-stream-data-range.md)的单个 DirectMusic pin。 DMusic 筛选器将从 DirectMusic 系统组件接收带时间戳的 MIDI 流的输入，并将 PCM 波纹流输出到 KMixer 系统驱动程序。 DMusic 驱动程序在内部混合其所有声音，以形成一个带有 PCM 波纹格式的双通道输出流。 DirectMusic 应用程序必须明确选择内核模式软件合成程序 Dmusic，以使用它来代替 DirectMusic 默认的用户模式合成。

### <a name="span-idaec_system_driverspanspan-idaec_system_driverspanaec-system-driver"></a><span id="aec_system_driver"></span><span id="AEC_SYSTEM_DRIVER"></span>AEC 系统驱动程序

AEC 系统驱动程序（DirectSound）通过在软件中实现 AEC （声音回声取消）和干扰干扰算法，支持全双工的应用程序。 有关详细信息，请参阅[DirectSound 捕获效果](directsound-capture-effects.md)。

### <a name="span-iddrmk_system_driverspanspan-iddrmk_system_driverspandrmk-system-driver"></a><span id="drmk_system_driver"></span><span id="DRMK_SYSTEM_DRIVER"></span>DRMK 系统驱动程序

DRMK 系统驱动程序（Drmk）是用于解密包含受 DRM 保护的内容的音频流的 KS 筛选器。 有关详细信息，请参阅[数字 Rights Management](digital-rights-management.md)。

### <a name="span-idsplitter_system_driverspanspan-idsplitter_system_driverspansplitter-system-driver"></a><span id="splitter_system_driver"></span><span id="SPLITTER_SYSTEM_DRIVER"></span>拆分系统驱动程序

拆分器系统驱动程序（node.js）是一个 KS 筛选器，它从单个输入捕获流创建两个或更多个输出流。 拆分器驱动程序以透明方式将输入流复制到与输入流格式无关的两个输出流。

Windows Me 和 Microsoft Windows XP 及更高版本支持拆分器驱动程序。 有关详细信息，请参阅[AVStream 拆分](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-splitters)器。

### <a name="span-idport_class_adapter_driver_and_portcls_system_driverspanspan-idport_class_adapter_driver_and_portcls_system_driverspanport-class-adapter-driver-and-portcls-system-driver"></a><span id="port_class_adapter_driver_and_portcls_system_driver"></span><span id="PORT_CLASS_ADAPTER_DRIVER_AND_PORTCLS_SYSTEM_DRIVER"></span>端口类适配器驱动程序和 PortCls 系统驱动程序

端口类适配器驱动程序使用端口/微型端口驱动程序体系结构来支持音频设备。 PortCls 驱动程序包含对 ISA 和 PCI 音频设备的内置驱动程序支持。 尽管 PortCls 系统驱动程序（Portcls）也为供应商提供的端口类适配器驱动程序提供框架，但是 Microsoft 建议供应商使用系统提供的端口类适配器驱动程序来支持 ISA 和 PCI 音频设备。 对于在其他硬件总线上构造音频设备的驱动程序或仅用于软件的设备，PortCls 框架可能也很有用。 有关详细信息，请参阅[端口类简介](introduction-to-port-class.md)。

### <a name="span-idusbaudio_class_system_driverspanspan-idusbaudio_class_system_driverspanusb-audio-class-system-driver-usbaudiosys"></a><span id="usbaudio_class_system_driver"></span><span id="USBAUDIO_CLASS_SYSTEM_DRIVER"></span>USB 音频类系统驱动程序（Usbaudio）

USBAudio 类系统驱动程序（Usbaudio）为符合音频设备的通用串行总线设备类定义的 USB 音频设备提供驱动程序支持。 有关此类系统驱动程序的详细信息，请参阅[USB 音频类系统驱动程序（Usbaudio）](usb-audio-class-system-driver--usbaudio-sys-.md)。

### <a name="span-idavcaudio_class_system_driverspanspan-idavcaudio_class_system_driverspanavcaudio-class-system-driver"></a><span id="avcaudio_class_system_driver"></span><span id="AVCAUDIO_CLASS_SYSTEM_DRIVER"></span>AVCAudio 类系统驱动程序

AVCAudio 类系统驱动程序（Avcaudio）是一种 AVStream 微型驱动程序，它为驻留在 IEEE 1394 总线上的音频设备提供驱动程序支持。 Windows XP 和更高版本中提供了适用于 IEEE 1394 音频设备的 AVCAudio 驱动程序和关联的支持。

若要使用系统提供的驱动程序，硬件供应商应设计其音频设备，以符合以下规范的相应部分：

-   IEC 61883-1 和 IEC 61883-6 （IEC 60958）

-   AV/C 数字接口命令集常规规范版本。 3.0

-   AV/C 音频子单位规范1。0

-   连接和兼容性管理规范1。0

-   AV/C 媒体流格式信息和协商

-   当前正在处理的 AV/C 音频子单元规范的更新

这些规范可在[1394 商业协会](https://go.microsoft.com/fwlink/p/?linkid=8728)网站上找到。 AVCAudio 驱动程序支持在这些规范中介绍的功能的子集。

当音频设备在即插即用设备枚举过程中将自身标识为符合 IEEE 1394 的音频设备时，系统会自动加载 AVCAudio 驱动程序来驱动设备。 AVCAudio 直接驱动设备，无需借助专用适配器驱动程序。 这意味着符合相应 IEEE 1394 规范的设备不需要专用适配器驱动程序。

Microsoft 建议硬件供应商对其 IEEE 1394 音频设备使用 AVCAudio 驱动程序，而不是编写专用的适配器驱动程序。

下图显示了 Windows XP 中的 IEEE 1394 音频设备的驱动程序层次结构。 在 Windows XP 及更高版本中，此图中所示的所有驱动程序组件都由 Microsoft 提供操作系统。

![说明1394音频设备的驱动程序层次结构的示意图](images/avcaudio.png)

有关图中的驱动程序组件的详细信息，请参阅以下部分：

[AVStream 概述](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)

[AV/C 客户端驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)

[IEEE 1394 总线](https://developer.microsoft.com/windows/hardware)

 

 




