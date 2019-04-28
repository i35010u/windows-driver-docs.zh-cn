---
title: 为音频适配器安装设备接口
description: 为音频适配器安装设备接口
ms.assetid: 824cc6a2-702a-4e51-91b1-ab776b1babf1
keywords:
- 音频适配器 WDK，设备接口
- 适配器驱动程序 WDK 音频设备接口
- 端口类音频适配器 WDK，设备接口
- 设备接口 WDK 音频
- 子设备 WDK 音频
- 音频设备接口 WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eaa23ba599e5afdd4e7b36817619ba67112f09d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333463"
---
# <a name="installing-device-interfaces-for-an-audio-adapter"></a>为音频适配器安装设备接口


## <span id="installing_device_interfaces_for_an_audio_adapter"></span><span id="INSTALLING_DEVICE_INTERFACES_FOR_AN_AUDIO_ADAPTER"></span>


客户端访问音频设备通过一系列*设备接口*的供应商指定适配器的 INF 文件中。 INF 文件中指定的设备接口具有一对一的对应关系与适配器驱动程序创建时初始化设备子设备 (请参阅[子创建](subdevice-creation.md))。 对于每个设备接口，该 INF 文件指定**FriendlyName**条目值，该值是在用户模式下，接口的注册表项下可访问。

在内核流体系结构，拓扑类别 (请参阅[ **KSPROPERTY\_拓扑\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff565799)) 表示设备接口的类。

下表列出了拓扑类别音频适配器是最有可能要用来描述其子设备的功能。

|Category|描述|
|--- |--- |
|KSCATEGORY_ACOUSTIC_ECHO_CANCEL|可以执行回声的音频设备 (请参阅[DirectSound 捕获效果](directsound-capture-effects.md)) 自行注册此类别下。|
|KSCATEGORY_AUDIO|所有音频设备将自行注册此类别下。|
|KSCATEGORY_CAPTURE|可以捕获的数据流的音频设备将自身注册此类别下。|
|KSCATEGORY_DATATRANSFORM|在流执行数据转换将音频设备将自身注册此类别下。|
|KSCATEGORY_MIXER|可以混合使用数据流将音频设备将自身注册此类别下。|
|KSCATEGORY_RENDER|音频设备可以呈现的数据流将自身注册此类别下。|
|KSCATEGORY_SYNTHESIZER|音频设备，可以将转换 MIDI 消息以或者波形音频示例或模拟输出信号将自身注册此类别下 (请参阅[合成和批接收器](synthesizers-and-wave-sinks.md))。|
|KSCATEGORY_TOPOLOGY|设备的[拓扑微型端口驱动程序](topology-miniport-driver.md)自行注册此类别下。|
|KSCATEGORY_DRM_DESCRAMBLE|可以对受 DRM 保护的批流进行解码的音频设备将自身注册此类别下 (请参阅[数字权限管理](digital-rights-management.md))。|


拓扑类别的完整列表，请参阅 KSCATEGORY\_*XXX* Ks.h 或 Ksmedia.h 的标头文件中定义的 Guid。

所有音频设备下 KSCATEGORY 进行分类\_音频，但将音频设备也可能属于在其他类别，如 KSCATEGORY\_（对于音频呈现设备） 的呈现器或 KSCATEGORY\_合成器（适用于合成）。 为每个类别的 INF 文件指定的设备，Windows 安装程序生成的一组设备类别名称下的注册表项 (请参阅[筛选器工厂](filter-factories.md))。

仅包含内置合成器的设备应将自己注册类别 KSCATEGORY 下\_合成器。 请注意此类别不包括纯 MPU 401 设备。 纯 MPU 401 设备，可以在输出或输入原始 MIDI 到或从 UART，应注册这些类别下：

-   KSCATEGORY\_音频

-   KSCATEGORY\_呈现

-   KSCATEGORY\_捕获

请注意， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)保留注册表类别 KSCATEGORY\_音频\_设备专用于其[虚拟音频设备](virtual-audio-devices.md)。 适配器驱动程序不应注册本身在此类别中。

下面的示例将安装适配器通常支持的音频设备的四个常见的系统定义的设备接口。

### <a name="span-idexampleinstallingaudiodeviceinterfacesspanspan-idexampleinstallingaudiodeviceinterfacesspanexample-installing-audio-device-interfaces"></a><span id="example__installing_audio_device_interfaces"></span><span id="EXAMPLE__INSTALLING_AUDIO_DEVICE_INTERFACES"></span>示例：安装的音频设备接口

在此示例中，使用 XYZ 音频设备的设备安装部分[ **INF AddInterface 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546310)安装四个音频适配器接口。 在下面的示例，每个四个指令将唯一引用字符串分配给一个接口，适配器驱动程序可用来区分每个接口类的实例。

```inf
  [XYZ-Audio-Device.Interfaces]
  AddInterface=%KSCATEGORY_AUDIO%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_RENDER%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_CAPTURE%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_TOPOLOGY%,%KSName_Topology%,XYZ-Audio-Device.Topology
```

前三个**AddInterface**指令指定名为 XYZ 音频 Device.Wave 添加接口部分。 最后一个指定名为 XYZ 音频 Device.Topology 添加接口部分。 每个添加接口部分将以下注册表项添加到设备接口子项，这是在用户模式下可访问\\DeviceClasses\\&lt;*InterfaceGUID* &gt;注册表项：

-   FriendlyName 注册表项指定每个设备接口的友好名称。

-   Microsoft DirectShow 要求设置为 GUID 值，该值指示可以访问和控制 KSProxy 系统驱动程序的适配器的代理的 CLSID 注册表项。

在下面的示例，其中包含向注册表添加每个接口的友好名称和 CLSID 的 INF 文件条目出现的两个添加接口部分：

```inf
  [XYZ-Audio-Device.Wave]
  AddReg=XYZ-Audio-Device.Wave.AddReg
  [XYZ-Audio-Device.Wave.AddReg]
  HKR,,FriendlyName,,%WaveDeviceName%
  HKR,,CLSID,,%Proxy.CLSID%

  [XYZ-Audio-Device.Topology]
  AddReg=XYZ-Audio-Device.Topology.AddReg
  [XYZ-Audio-Device.Topology.AddReg]
  HKR,,FriendlyName,,%WaveDeviceMixerName%
  HKR,,CLSID,,%Proxy.CLSID%
```

在此示例中的关键字 HKR 表示设备的系统提供的注册表路径。 有关详细信息，请参阅[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。

下面是此示例中的字符串部分。

```inf
  [Strings]
  KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
  KSCATEGORY_RENDER="{65E8773E-8F56-11D0-A3B9-00A0C9223196}"
  KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"
  KSCATEGORY_TOPOLOGY="{DDA54A40-1E4C-11D1-A050-405705C10000}"
  Proxy.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
  WaveDeviceName="XYZ Audio Device"
  WaveDeviceMixerName="XYZ Audio Device Super Mixer"
```

该字符串命名**AddInterface**指令指定 KSCATEGORY\_*XXX*设备接口不能进行本地化，因为适配器驱动程序使用相同的名称在内部为字符串常量。 Windows Driver Kit (WDK) 中的示例适配器驱动程序使用其音频设备接口的以下字符串名称：

```inf
  KSNAME_Wave="Wave"
  KSNAME_UART="UART"
  KSNAME_FMSynth="FMSynth"
  KSNAME_Topology="Topology"
  KSNAME_Wavetable="Wavetable"
  KSNAME_DMusic="DMusic"
```

出于一致性需要，专用驱动程序应将这些相同的名称分配给其相应的设备接口。 如果您的驱动程序支持是专用的其他设备接口，可以创建自己的专有名称，这些接口。 请确保驱动程序使用的名称匹配 INF 文件中。 如果字符串不匹配，system 安装程序不会加载该驱动程序。

