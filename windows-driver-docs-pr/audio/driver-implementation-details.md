---
title: 驱动程序实现详细信息
description: 本主题介绍为能够处理硬件卸载音频流的音频适配器开发的音频驱动程序的实现细节。
ms.date: 04/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1357fe4ad38fd4352b263379090a7412632c8695
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789255"
---
# <a name="driver-implementation-details"></a>驱动程序实现详细信息


本主题介绍为能够处理硬件卸载音频流的音频适配器开发的音频驱动程序的实现细节。

换句话说，本主题介绍 Microsoft 从 Windows 8) 开始 (的操作，以支持可处理硬件卸载音频的音频适配器的驱动程序。 在以下各节中，本主题还说明了驱动程序必须支持此类适配器的能力。

## <a name="span-ida__new_type_guid_for_node_descriptorsspanspan-ida__new_type_guid_for_node_descriptorsspanspan-ida__new_type_guid_for_node_descriptorsspana-new-type-guid-for-node-descriptors"></a><span id="A__new_Type_GUID_for_node_descriptors"></span><span id="a__new_type_guid_for_node_descriptors"></span><span id="A__NEW_TYPE_GUID_FOR_NODE_DESCRIPTORS"></span>节点描述符的新 *类型* GUID


如果音频适配器能够处理卸载的音频流，则适配器的音频驱动程序将使用适配器的 KS 筛选器中新引入的节点来公开此功能。

音频流路径中的每个节点都有一个节点描述符，因此，对于此新节点，驱动程序必须将 *类型* GUID 设置为 [**KSNODETYPE \_ audio \_ ENGINE**](./ksnodetype-audio-engine.md)。 下面的示例演示了驱动程序如何为此新节点配置节点描述符：

```ManagedCPlusPlus
typedef struct _KSNODE_DESCRIPTOR {
  const KSAUTOMATION_TABLE *AutomationTable;    // drv specific
  const GUID               *Type;       // must be set to KSNODETYPE_AUDIO_ENGINE
  const GUID               *Name;       // drv specific (KSNODETYPE_AUDIO_ENGINE?)  
} KSNODE_DESCRIPTOR, *PKSNODE_DESCRIPTOR;
```

如果名称 GUID 设置为 **KSNODETYPE \_ 音频 \_ 引擎**，则必须为此节点创建默认名称字符串。 然后，将该字符串添加到 *ks*，以便在安装驱动程序的过程中，该字符串可用于填充 HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Control \\ MediaCategories 注册表项。

新节点类型 **KSNODETYPE \_ 音频 \_ 引擎** 的 GUID 定义如下所示：

```ManagedCPlusPlus
Code style
#define STATIC_KSNODETYPE_AUDIO_ENGINE\
    0x35caf6e4, 0xf3b3, 0x4168, 0xbb, 0x4b, 0x55, 0xe7, 0x7a, 0x46, 0x1c, 0x7e
DEFINE_GUIDSTRUCT("35CAF6E4-F3B3-4168-BB4B-55E77A461C7E", KSNODETYPE_AUDIO_ENGINE);
#define KSNODETYPE_AUDIO_ENGINE DEFINE_GUIDNAMED(KSNODETYPE_AUDIO_ENGINE)
```

有关详细信息，请参阅 *ksmedia* 头文件。

基于上述信息，微型端口节点的描述符可能如下所示：

```ManagedCPlusPlus
PCNODE_DESCRIPTOR MiniportNodes[] =
{
    // KSNODE_WAVE_AUDIO_ENGINE
    {
        0,                          // Flags
        NULL,                       // AutomationTable
        &KSNODETYPE_AUDIO_ENGINE,   // Type  KSNODETYPE_AUDIO_ENGINE
        NULL                        // Name
    }
};
```

## <a name="span-ida_new_ks_property_set_for_audio_enginesspanspan-ida_new_ks_property_set_for_audio_enginesspanspan-ida_new_ks_property_set_for_audio_enginesspana-new-ks-property-set-for-audio-engines"></a><span id="A_new_KS_property_set_for_audio_engines"></span><span id="a_new_ks_property_set_for_audio_engines"></span><span id="A_NEW_KS_PROPERTY_SET_FOR_AUDIO_ENGINES"></span>为音频引擎设置新的 KS 属性


从 Windows 8 开始，引入了 [KSPROPSETID \_ AudioEngine](./kspropsetid-audioengine.md) 属性集，以支持硬件音频引擎和硬件卸载音频处理。 因此，可以处理卸载的音频流的适配器的驱动程序必须支持此新属性集中的属性。

新属性集 **KSPROPSETID \_ AudioEngine** 定义如下：

```ManagedCPlusPlus
#define STATIC_KSPROPSETID_AudioEngine\
    0x3A2F82DCL, 0x886F, 0x4BAA, 0x9E, 0xB4, 0x8, 0x2B, 0x90, 0x25, 0xC5, 0x36
DEFINE_GUIDSTRUCT("3A2F82DC-886F-4BAA-9EB4-082B9025C536", KSPROPSETID_AudioEngine);
#define KSPROPSETID_AudioEngine DEFINE_GUIDNAMED(KSPROPSETID_AudioEngine)
```

此新属性集中的属性名称在 [**KSPROPERTY \_ AUDIOENGINE**](./ksproperty-audioengine.md) 枚举中定义，驱动程序必须支持这些名称。

下面是 **KSPROPSETID \_ AudioEngine** 属性集中的新属性：

[**KSPROPERTY \_ AUDIOENGINE \_ 缓冲区 \_ 大小 \_ 范围**](./ksproperty-audioengine-buffer-size-limits.md)

[**KSPROPERTY \_ AUDIOENGINE \_ 描述符**](./ksproperty-audioengine-descriptor.md)

[**KSPROPERTY \_ AUDIOENGINE \_ DEVICEFORMAT**](./ksproperty-audioengine-deviceformat.md)

[**KSPROPERTY \_ AUDIOENGINE \_ GFXENABLE**](./ksproperty-audioengine-gfx-enable.md)

[**KSPROPERTY \_ AUDIOENGINE \_ LFXENABLE**](./ksproperty-audioengine-lfx-enable.md)

[**KSPROPERTY \_ AUDIOENGINE \_ 环回 \_ 保护**](./ksproperty-audioengine-loopback-protection.md)

[**KSPROPERTY \_ AUDIOENGINE \_ MIXFORMAT**](./ksproperty-audioengine-mixformat.md)

[**KSPROPERTY \_ AUDIOENGINE \_ SUPPORTEDDEVICEFORMATS**](./ksproperty-audioengine-supporteddeviceformats.md)

[**KSPROPERTY \_ AUDIOENGINE \_ VOLUMELEVEL**](./ksproperty-audioengine-volumelevel.md)

## <a name="span-idupdates_to_the_kspropsetid__audio_property_setspanspan-idupdates_to_the_kspropsetid__audio_property_setspanspan-idupdates_to_the_kspropsetid__audio_property_setspanupdates-to-the-kspropsetid_-audio-property-set"></a><span id="Updates_to_the_KSPROPSETID__Audio_property_set"></span><span id="updates_to_the_kspropsetid__audio_property_set"></span><span id="UPDATES_TO_THE_KSPROPSETID__AUDIO_PROPERTY_SET"></span>更新 KSPROPSETID \_ Audio 属性集


除了支持 new **KSPROPSETID \_ AudioEngine** 属性集中的属性以外，驱动程序还必须支持 [KSPROPSETID \_ 音频](./kspropsetid-audio.md) 属性集中的以下现有属性：

[**KSPROPERTY \_ 音频 \_ 静音**](./ksproperty-audio-mute.md)

[**KSPROPERTY \_ 音频 \_ PEAKMETER2**](./ksproperty-audio-peakmeter2.md)

[**KSPROPERTY \_ 音频 \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md)

为了完成对硬件卸载音频处理的驱动程序支持的实现，已向 **KSPROPSETID \_ audio** 属性集添加了新属性。

下面是新的 **KSPROPSETID \_ 音频** 属性：

[**KSPROPERTY \_ 音频 \_ 线性 \_ 缓冲区 \_ 位置**](./ksproperty-audio-linear-buffer-position.md)

[**KSPROPERTY \_ 音频 \_ 演示 \_ 位置**](./ksproperty-audio-presentation-position.md)

[**KSPROPERTY \_ 音频 \_ WAVERT \_ 当前 \_ 写入 \_ 位置**](./ksproperty-audio-wavert-current-write-position.md)

## <a name="span-idport-class_driver_updates_and_glitch_reportingspanspan-idport-class_driver_updates_and_glitch_reportingspanspan-idport-class_driver_updates_and_glitch_reportingspanport-class-driver-updates-and-glitch-reporting"></a><span id="Port-class_driver_updates_and_glitch_reporting"></span><span id="port-class_driver_updates_and_glitch_reporting"></span><span id="PORT-CLASS_DRIVER_UPDATES_AND_GLITCH_REPORTING"></span>端口类驱动程序更新和故障报告


除了前面部分中介绍的对硬件卸载音频处理的支持外，Windows 端口级驱动程序还使用 "帮助程序接口" 进行了更新，使开发可用于卸载的音频流的驱动程序更简单。 当此类驱动程序检测到故障时，有一种机制可让驱动程序报告故障错误。 以下主题提供了有关帮助程序接口和故障报告的更多详细信息：

[用于已卸载音频的处理的帮助程序接口](helper-interfaces-for-offloaded-audio-processing.md)

[已卸载音频的故障报告](glitch-reporting-for-offloaded-audio.md)

 

