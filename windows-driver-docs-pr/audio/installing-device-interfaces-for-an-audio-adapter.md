---
title: 为音频适配器安装设备接口
description: 为音频适配器安装设备接口
ms.assetid: 824cc6a2-702a-4e51-91b1-ab776b1babf1
keywords:
- 音频适配器 WDK，设备接口
- 适配器驱动程序 WDK 音频，设备接口
- 端口类音频适配器 WDK，设备接口
- 设备接口 WDK 音频
- subdevices WDK 音频
- 音频设备接口 WDK
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb53c185b24a1f0462c5f58ea527b358472663cf
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207043"
---
# <a name="installing-device-interfaces-for-an-audio-adapter"></a>为音频适配器安装设备接口


## <span id="installing_device_interfaces_for_an_audio_adapter"></span><span id="INSTALLING_DEVICE_INTERFACES_FOR_AN_AUDIO_ADAPTER"></span>


客户端通过一组由供应商在适配器的 INF 文件中指定的 *设备接口* 访问音频设备。 INF 文件中指定的设备接口与适配器驱动程序在初始化设备时创建的 subdevices 之间存在一一对应关系 (请参阅 [Subdevice 创建](subdevice-creation.md)) 。 对于每个设备接口，INF 文件指定 **FriendlyName** 条目值，该值可在用户模式下的接口注册表项下访问。

在内核流式处理体系结构中，拓扑类别 (参阅 [**KSPROPERTY \_ 拓扑 \_ 类别**](../stream/ksproperty-topology-categories.md)) 表示设备接口类。

下表列出了音频适配器最有可能用于说明其 subdevices 功能的拓扑类别。

|类别|说明|
|--- |--- |
|KSCATEGORY_ACOUSTIC_ECHO_CANCEL|可以执行声音回声取消的音频设备 (参阅 [DirectSound 捕获效果](directsound-capture-effects.md)) 在此类别下注册自身。|
|KSCATEGORY_AUDIO|所有音频设备会自行注册此类别。|
|KSCATEGORY_CAPTURE|可以捕获数据流的音频设备会自行注册此类别。|
|KSCATEGORY_DATATRANSFORM|在流上执行数据转换的音频设备会在此类别下注册自身。|
|KSCATEGORY_MIXER|可以混合使用的音频设备会在此类别下注册自身。|
|KSCATEGORY_RENDER|可以呈现数据流的音频设备会在此类别下进行注册。|
|KSCATEGORY_SYNTHESIZER|一种音频设备，可将 MIDI 消息转换为波形音频样本或模拟输出信号会自行注册到此类别 (请参阅) 的 [合成和波形接收器](synthesizers-and-wave-sinks.md) 。|
|KSCATEGORY_TOPOLOGY|设备的 [拓扑微型端口驱动程序](topology-miniport-driver.md) 会自行注册此类别。|
|KSCATEGORY_DRM_DESCRAMBLE|可以对受 DRM 保护的波形流进行译码的音频设备会在此类别下注册自身 (请参阅 [数字 Rights Management](digital-rights-management.md)) 。|


有关拓扑类别的完整列表，请参阅 \_ 头文件 Ks 和 Ksmedia 中定义的 KSCATEGORY*XXX* guid。

所有音频设备都在 KSCATEGORY 音频下进行分类 \_ ，但音频设备还可能会分类到 \_) 或 KSCATEGORY \_ 合成器 (为合成器) 的其他类别，如 KSCATEGORY RENDER (。 对于 INF 文件为设备指定的每个类别，Windows Installer 会在类别名称下为该设备生成一组注册表项， (参阅 [筛选器工厂](filter-factories.md)) 。

只有包含内置合成器的设备才应在 KSCATEGORY 合成器类别下进行注册 \_ 。 请注意，此类别不包括纯 MPU-401 设备。 纯粹的 MPU-401 设备（可从 UART 输出或输入原始 MIDI）应自行注册到以下类别：

-   KSCATEGORY \_ 音频

-   KSCATEGORY \_ 呈现

-   KSCATEGORY \_ 捕获

请注意， [SysAudio 系统驱动程序](kernel-mode-wdm-audio-components.md#sysaudio_system_driver) \_ \_ 为其 [虚拟音频设备](virtual-audio-devices.md)保留注册表类别 KSCATEGORY 音频设备。 适配器驱动程序不应在此类别中注册自身。

下面的示例将安装四个常见的系统定义的设备接口，适配器通常为音频设备提供支持。

### <a name="span-idexample__installing_audio_device_interfacesspanspan-idexample__installing_audio_device_interfacesspanexample-installing-audio-device-interfaces"></a><span id="example__installing_audio_device_interfaces"></span><span id="EXAMPLE__INSTALLING_AUDIO_DEVICE_INTERFACES"></span>示例：安装音频设备接口

在此示例中，XYZ 音频设备的设备安装部分使用 [**INF AddInterface 指令**](../install/inf-addinterface-directive.md) 安装四个音频适配器接口。 在下面的示例中，四个指令将一个唯一的引用字符串分配给接口，适配器驱动程序可以使用该字符串来区分每个接口类的实例。

```inf
  [XYZ-Audio-Device.Interfaces]
  AddInterface=%KSCATEGORY_AUDIO%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_RENDER%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_CAPTURE%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_TOPOLOGY%,%KSName_Topology%,XYZ-Audio-Device.Topology
```

前三个 **AddInterface** 指令指定名为 "XYZ-音频设备" 的添加接口部分。 最后指定一个名为 "XYZ-Audio-设备" 的添加接口部分。 每个添加接口部分将以下注册表项添加到设备接口子项，该子项可在用户模式下的 \\ DeviceClasses \\ &lt; *InterfaceGUID* &gt; 注册表项下访问：

-   FriendlyName 注册表项指定每个设备接口的友好名称。

-   Microsoft DirectShow 需要 CLSID 注册表项，并将其设置为代理 GUID 值，这指示该适配器可以通过 KSProxy 系统驱动程序进行访问和控制。

下面的示例显示了两个添加接口部分，其中包含将每个接口的 FriendlyName 和 CLSID 添加到注册表的 INF 文件条目：

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

在此示例中，关键字 HKR 表示设备的系统提供的注册表路径。 有关详细信息，请参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)。

下面是此示例的字符串部分。

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

**AddInterface**指令为 KSCATEGORY XXX 设备接口指定的字符串名称 \_ *XXX*不能进行本地化，因为适配器驱动程序在内部使用与字符串常量相同的名称。 Windows 驱动程序工具包中的示例适配器驱动程序 (WDK) 为其音频设备接口使用以下字符串名称：

```inf
  KSNAME_Wave="Wave"
  KSNAME_UART="UART"
  KSNAME_FMSynth="FMSynth"
  KSNAME_Topology="Topology"
  KSNAME_Wavetable="Wavetable"
  KSNAME_DMusic="DMusic"
```

为了保持一致性，你的专有驱动程序应将这些相同的名称分配给其相应的设备接口。 如果驱动程序支持专用的其他设备接口，则可以为这些接口提供自己的专有名称。 请确保驱动程序使用的名称与 INF 文件中的名称匹配。 如果字符串不匹配，则系统安装程序不会加载驱动程序。