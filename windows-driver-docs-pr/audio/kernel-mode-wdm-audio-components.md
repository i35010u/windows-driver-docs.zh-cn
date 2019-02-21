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
- 拆分器系统驱动程序 WDK 音频
- 端口类适配器驱动程序 WDK 音频
- USBAudio 类系统驱动程序 WDK 音频
- AVCAudio 类系统驱动程序 WDK 音频
- 1394 WDK 音频
- KMixer 系统驱动程序 WDK 音频，有关 KMixer 系统驱动程序
- IEEE 1394 WDK 音频
- WDM 音频组件 WDK
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 239c968d82da525c03967408201b73f5a8e9cb37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548136"
---
# <a name="kernel-mode-wdm-audio-components"></a>内核模式 WDM 音频组件


## <span id="kernel_mode_wdm_audio_components"></span><span id="KERNEL_MODE_WDM_AUDIO_COMPONENTS"></span>


内核模式下的 Microsoft Windows 驱动程序模型 (WDM) 音频组件包括：

WDMAud 系统驱动程序

SysAudio System Driver

KMixer 系统驱动程序

Redbook 系统驱动程序

SBEmul 系统驱动程序

SWMidi 系统驱动程序

DMusic 系统驱动程序

AEC 系统驱动程序

DRMK 系统驱动程序

拆分器系统驱动程序

端口类适配器驱动程序和 PortCls 系统驱动程序

USB 音频类系统驱动程序 (Usbaudio.sys)

AVCAudio 类系统驱动程序

### <a name="span-idkmwdmaudsystemdriverspanspan-idkmwdmaudsystemdriverspanwdmaud-system-driver"></a><span id="km_wdmaud_system_driver"></span><span id="KM_WDMAUD_SYSTEM_DRIVER"></span>WDMAud 系统驱动程序

内核模式 WDMAud 系统驱动程序 (Wdmaud.sys) 与用户模式下 WDMAud 系统驱动程序 (Wdmaud.drv) 配对。 WDMAud 驱动程序对用户模式下 Microsoft Windows 多媒体系统调用和内核流式处理 I/O 请求之间进行转换。 WDMAud 执行 I/O 的以下 Api: **waveIn**， **waveOut**， **midiIn**， **midiOut**， **mixer**，并**aux** （Microsoft Windows SDK 文档中所述）。 内核模式 WDMAud 驱动程序是流式处理 (KS) 筛选器和 SysAudio 系统驱动程序的客户端的内核。

### <a name="span-idsysaudiosystemdriverspanspan-idsysaudiosystemdriverspansysaudio-system-driver"></a><span id="sysaudio_system_driver"></span><span id="SYSAUDIO_SYSTEM_DRIVER"></span>SysAudio 系统驱动程序

SysAudio 系统驱动程序 (Sysaudio.sys) 生成筛选器关系图的呈现和捕获音频内容。 SysAudio 驱动程序表示作为音频筛选器图形[音频的虚拟设备](virtual-audio-devices.md)并将每个虚拟的音频设备注册为实例 KSCATEGORY\_音频\_设备设备接口。 （适配器驱动程序不应注册自己以独占方式为 SysAudio 保留此类别中。）例如，虚拟 MIDI 设备可能表示通过连接 SWMidi 驱动程序、 KMixer 驱动程序和端口/微型端口驱动程序创建的筛选器关系图。 客户端通信仅使用虚拟的音频设备而不是使用组成虚拟音频设备的单个设备。 透明的客户端，SysAudio 驱动程序配置所有 KS 筛选器连接在一起以形成虚拟的音频设备的筛选器关系图中。 以下的音频流源使用 SysAudio 生成关系图：

-   DirectSound （请参阅 Microsoft Windows SDK 文档。）

-   Windows 多媒体 Api **waveIn**， **waveOut**， **midiIn**， **midiOut**， **mixer**，和**aux** （请参阅 Windows SDK 文档。）

-   Redbook CD 数字音频 （请参阅 Redbook 系统驱动程序。）

-   听起来 Blaster 仿真程序 （请参阅 SBEmul 系统驱动程序。）

-   内核模式软件合成器 （请参阅 SWMidi 系统驱动程序和 DMusic 系统驱动程序。）

-   DRMK 系统驱动程序

### <a name="span-idkmixersystemdriverspanspan-idkmixersystemdriverspankmixer-system-driver"></a><span id="kmixer_system_driver"></span><span id="KMIXER_SYSTEM_DRIVER"></span>KMixer 系统驱动程序

KMixer 系统驱动程序 (Kmixer.sys) 是 KS 筛选器，执行以下任务：

-   混合的多个 PCM 音频流

-   高质量格式转换

-   位深度转换

-   扬声器配置和通道映射

除了简单 8 位和 16 位，mono 和立体声数据格式 KMixer 驱动程序支持：

-   PCM 和 IEEE 浮点数据

-   位深度大于 16 位，且具有两个以上声道的多渠道格式

-   Head 相关传输函数 (HRTF) 三维处理

有关卷范围和各种版本的 Windows 中的默认卷级别的信息，请参阅[默认音频音量设置](default-audio-volume-settings.md)。

### <a name="span-idredbooksystemdriverspanspan-idredbooksystemdriverspanredbook-system-driver"></a><span id="redbook_system_driver"></span><span id="REDBOOK_SYSTEM_DRIVER"></span>Redbook 系统驱动程序

Redbook 系统驱动程序 (Redbook.sys) 是 KS 筛选器，用于管理数字音频 CD 的呈现。 Redbook 驱动程序是 SysAudio 系统驱动程序的客户端。 系统路由通过文件系统的 CD 数字音频到 Redbook 驱动程序，再到 SysAudio 驱动程序。 CD 数字音频是首选的 wave 输出设备上呈现 （为在控制面板中的多媒体属性页中设置）。

### <a name="span-idsbemulsystemdriverspanspan-idsbemulsystemdriverspansbemul-system-driver"></a><span id="sbemul_system_driver"></span><span id="SBEMUL_SYSTEM_DRIVER"></span>SBEmul 系统驱动程序

SBEmul 系统驱动程序 (Sbemul.sys) 提供了用于 MS-DOS 应用程序的声音 Blaster 仿真。 SBEmul 驱动程序是 SysAudio 系统驱动程序的客户端。 若要呈现并捕获内容，SysAudio 驱动程序使用的首选的批和 MIDI 设备 （与在控制面板中的多媒体属性页中设置）。

仅在 Windows 98 中支持声音 Blaster 仿真 / me 一起提供。

### <a name="span-idswmidisystemdriverspanspan-idswmidisystemdriverspanswmidi-system-driver"></a><span id="swmidi_system_driver"></span><span id="SWMIDI_SYSTEM_DRIVER"></span>SWMidi 系统驱动程序

SWMidi 系统驱动程序 (Swmidi.sys) 是提供软件模拟常规 MIDI (GM) 和高质量 Roland GS 波表合成 KS 筛选器。 一个 **midiOut * * * Xxx*硬件合成器不可用时，应用程序使用 SWMidi。 SWMidi 筛选器作为输入加盖时间戳 MIDI 从接收流 WDMAud 系统驱动程序，并输出到 KMixer 系统驱动程序的 PCM 批流。 SWMidi 混合使用所有其语音在内部以形成 PCM 声波格式的单个两个通道输出流。

### <a name="span-iddmusicsystemdriverspanspan-iddmusicsystemdriverspandmusic-system-driver"></a><span id="dmusic_system_driver"></span><span id="DMUSIC_SYSTEM_DRIVER"></span>DMusic 系统驱动程序

DMusic 系统驱动程序 (Dmusic.sys) 是支持软件模拟、 高质量、 可下载声音 (DL) 合成 KS 筛选器。 DMusic 驱动程序是一个系统提供的端口类微型端口驱动程序。 它公开单个 DirectMusic 插针，它支持[DirectMusic 流式传输的数据范围](directmusic-stream-data-range.md)。 DMusic 筛选器作为输入加盖时间戳 MIDI 从接收流 DirectMusic 系统组件，并输出到 KMixer 系统驱动程序的 PCM 批流。 DMusic 驱动程序混合使用所有其语音在内部以形成 PCM 声波格式的单个两个通道输出流。 DirectMusic 应用程序必须明确选择内核模式软件合成器 Dmusic.sys，来代替 DirectMusic 的默认情况下，用户模式下合成器。

### <a name="span-idaecsystemdriverspanspan-idaecsystemdriverspanaec-system-driver"></a><span id="aec_system_driver"></span><span id="AEC_SYSTEM_DRIVER"></span>AEC 系统驱动程序

AEC 系统驱动程序 (Aec.sys) 通过在软件中实现 AEC （回声抵消） 和干扰抑制算法支持全双工 DirectSound 应用程序。 有关详细信息，请参阅[DirectSound 捕获效果](directsound-capture-effects.md)。

### <a name="span-iddrmksystemdriverspanspan-iddrmksystemdriverspandrmk-system-driver"></a><span id="drmk_system_driver"></span><span id="DRMK_SYSTEM_DRIVER"></span>DRMK 系统驱动程序

DRMK 系统驱动程序 (Drmk.sys) 是 KS 筛选器，用于解密包含受 DRM 保护的内容的音频流。 有关详细信息，请参阅[数字权限管理](digital-rights-management.md)。

### <a name="span-idsplittersystemdriverspanspan-idsplittersystemdriverspansplitter-system-driver"></a><span id="splitter_system_driver"></span><span id="SPLITTER_SYSTEM_DRIVER"></span>拆分器系统驱动程序

拆分器系统驱动程序 (Splitter.sys) 是 KS 筛选器，创建两个或多个输出流的单个输入的捕获流。 拆分器驱动程序以透明方式将输入的流复制到两个独立于的输入流格式的详细输出流。

拆分器驱动程序是受 Windows Me 和 Microsoft Windows XP 及更高版本。 有关详细信息，请参阅[AVStream 拆分条](https://msdn.microsoft.com/library/windows/hardware/ff554255)。

### <a name="span-idportclassadapterdriverandportclssystemdriverspanspan-idportclassadapterdriverandportclssystemdriverspanport-class-adapter-driver-and-portcls-system-driver"></a><span id="port_class_adapter_driver_and_portcls_system_driver"></span><span id="PORT_CLASS_ADAPTER_DRIVER_AND_PORTCLS_SYSTEM_DRIVER"></span>端口类适配器驱动程序和 PortCls 系统驱动程序

端口类适配器驱动程序使用的端口/微型端口驱动程序体系结构来支持音频设备。 PortCls 驱动程序包括对 ISA 和 PCI 的音频设备的内置驱动程序支持。 尽管 PortCls 系统驱动程序 (Portcls.sys) 还提供了供应商提供端口类适配器驱动程序的框架，但 Microsoft 建议供应商使用系统提供的端口类适配器驱动程序来支持 ISA 和 PCI 的音频设备。 PortCls 框架也可能用于构造驱动程序的仅限软件的设备或其他硬件总线上的音频设备。 有关详细信息，请参阅[端口类简介](introduction-to-port-class.md)。

### <a name="span-idusbaudioclasssystemdriverspanspan-idusbaudioclasssystemdriverspanusb-audio-class-system-driver-usbaudiosys"></a><span id="usbaudio_class_system_driver"></span><span id="USBAUDIO_CLASS_SYSTEM_DRIVER"></span>USB 音频类系统驱动程序 (Usbaudio.sys)

USBAudio 类系统驱动程序 (Usbaudio.sys) 音频设备的通用串行总线设备类定义符合 USB 音频设备提供驱动程序支持。 有关此类系统驱动程序的详细信息，请参阅[USB 音频类系统驱动程序 (Usbaudio.sys)](usb-audio-class-system-driver--usbaudio-sys-.md)。

### <a name="span-idavcaudioclasssystemdriverspanspan-idavcaudioclasssystemdriverspanavcaudio-class-system-driver"></a><span id="avcaudio_class_system_driver"></span><span id="AVCAUDIO_CLASS_SYSTEM_DRIVER"></span>AVCAudio 类系统驱动程序

AVCAudio 类系统驱动程序 (Avcaudio.sys) 是提供驻留在的 IEEE 1394 总线的音频设备驱动程序支持 AVStream 微型驱动程序。 AVCAudio 驱动程序和关联的 IEEE 1394 音频设备的支持均可在 Windows XP 及更高版本。

若要使用系统提供的驱动程序，硬件供应商应该设计其音频设备以符合以下规范的相应部分：

-   IEC 61883 1 和 IEC 61883-6 (IEC 60958)

-   AV/C 数字接口命令设置常规规范 ver. 3.0

-   AV/C 音频子单元规范 1.0

-   连接和兼容性管理规范 1.0

-   AV/C 媒体 Stream 的格式信息和协商

-   更新过程中当前的 AV/C 音频子单元规范

这些规范是网址[1394年贸易协会](https://go.microsoft.com/fwlink/p/?linkid=8728)网站。 AVCAudio 驱动程序支持在这些规范中所述的功能的子集。

当音频设备将自身标识为 IEEE 1394 符合音频设备即插即用设备枚举期间时，系统会自动加载 AVCAudio 驱动程序来驱动设备。 AVCAudio 驱动器在设备直接，而无需专用适配器驱动程序的帮助。 这意味着符合相应的 IEEE 1394 规范的设备需要任何专有适配器驱动程序。

Microsoft 建议硬件供应商的 IEEE 1394 音频设备而不是编写专有适配器驱动程序使用 AVCAudio 驱动程序。

下图显示在 Windows XP IEEE 1394 音频设备的驱动程序层次结构。 在 Windows XP 及更高版本，所有在此图中所示的驱动程序组件是由 Microsoft 提供与操作系统。

![说明 1394年音频设备的驱动程序层次结构的关系图](images/avcaudio.png)

在图中的驱动程序组件有关的详细信息，请参阅以下各节：

[AVStream 概述](https://msdn.microsoft.com/library/windows/hardware/ff554240)

[AV/C 客户端驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff556364)

[IEEE 1394 总线](https://msdn.microsoft.com/library/windows/hardware/ff537207)

 

 




