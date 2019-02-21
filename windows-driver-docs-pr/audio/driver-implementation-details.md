---
title: 驱动程序实现详细信息
description: 本主题介绍了为能够处理硬件卸载音频流的音频适配器开发的音频驱动程序的实现详细信息。
ms.assetid: FB17FADD-D683-4ECC-95F9-86DF7A289C63
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11d7c2a0dbde495b6eeb27d30522445a84ba2c63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545119"
---
# <a name="driver-implementation-details"></a>驱动程序实现详细信息


本主题介绍了为能够处理硬件卸载音频流的音频适配器开发的音频驱动程序的实现详细信息。

换而言之，本主题说明什么 Microsoft 采取了措施 （从 Windows 8 开始） 来支持适用于能够处理硬件卸载音频的音频适配器的驱动程序。 在以下部分中，本主题还说明哪些驱动程序必须能够以支持此类适配器。

## <a name="span-idanewtypeguidfornodedescriptorsspanspan-idanewtypeguidfornodedescriptorsspanspan-idanewtypeguidfornodedescriptorsspana-new-type-guid-for-node-descriptors"></a><span id="A__new_Type_GUID_for_node_descriptors"></span><span id="a__new_type_guid_for_node_descriptors"></span><span id="A__NEW_TYPE_GUID_FOR_NODE_DESCRIPTORS"></span>一个新*类型*节点描述符的 GUID


如果音频适配器可处理卸载音频流，适配器的音频驱动程序公开此功能通过新引入的节点 KS 筛选器中使用的适配器。

音频流的路径中每个节点都是节点的描述符，因此驱动程序必须设置为此新节点*类型*GUID 传递给[ **KSNODETYPE\_音频\_引擎**](https://msdn.microsoft.com/library/windows/hardware/hh450866). 下面是如何驱动程序无法配置此新节点的节点描述符的示例：

```ManagedCPlusPlus
typedef struct _KSNODE_DESCRIPTOR {
  const KSAUTOMATION_TABLE *AutomationTable;    // drv specific
  const GUID               *Type;       // must be set to KSNODETYPE_AUDIO_ENGINE
  const GUID               *Name;       // drv specific (KSNODETYPE_AUDIO_ENGINE?)  
} KSNODE_DESCRIPTOR, *PKSNODE_DESCRIPTOR;
```

如果名称 GUID 设置为**KSNODETYPE\_音频\_引擎**，则必须创建此节点的默认名称字符串。 然后，添加到该字符串*ks.inf*，以便在安装期间，驱动程序，该字符串可用于填充 HKEY\_本地\_机\\系统\\CurrentControlSet\\控制\\MediaCategories 注册表项。

对于新的节点类型，GUID 的定义**KSNODETYPE\_音频\_引擎**，如下所示：

```ManagedCPlusPlus
Code style
#define STATIC_KSNODETYPE_AUDIO_ENGINE\
    0x35caf6e4, 0xf3b3, 0x4168, 0xbb, 0x4b, 0x55, 0xe7, 0x7a, 0x46, 0x1c, 0x7e
DEFINE_GUIDSTRUCT("35CAF6E4-F3B3-4168-BB4B-55E77A461C7E", KSNODETYPE_AUDIO_ENGINE);
#define KSNODETYPE_AUDIO_ENGINE DEFINE_GUIDNAMED(KSNODETYPE_AUDIO_ENGINE)
```

有关详细信息，请参阅*ksmedia.h*标头文件。

并根据上述信息，微型端口节点的描述符可能如下所示：

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

## <a name="span-idanewkspropertysetforaudioenginesspanspan-idanewkspropertysetforaudioenginesspanspan-idanewkspropertysetforaudioenginesspana-new-ks-property-set-for-audio-engines"></a><span id="A_new_KS_property_set_for_audio_engines"></span><span id="a_new_ks_property_set_for_audio_engines"></span><span id="A_NEW_KS_PROPERTY_SET_FOR_AUDIO_ENGINES"></span>新 KS 属性设置为音频引擎


从 Windows 8 开始[KSPROPSETID\_AudioEngine](https://msdn.microsoft.com/library/windows/hardware/hh450902)引入了属性集以支持硬件音频引擎和硬件卸载音频处理。 因此可以处理的适配器的驱动程序卸载音频流必须支持的属性中设置此新属性。

设置新属性， **KSPROPSETID\_AudioEngine**，定义如下：

```ManagedCPlusPlus
#define STATIC_KSPROPSETID_AudioEngine\
    0x3A2F82DCL, 0x886F, 0x4BAA, 0x9E, 0xB4, 0x8, 0x2B, 0x90, 0x25, 0xC5, 0x36
DEFINE_GUIDSTRUCT("3A2F82DC-886F-4BAA-9EB4-082B9025C536", KSPROPSETID_AudioEngine);
#define KSPROPSETID_AudioEngine DEFINE_GUIDNAMED(KSPROPSETID_AudioEngine)
```

在中定义此新设置的属性中的属性的名称[ **KSPROPERTY\_AUDIOENGINE** ](https://msdn.microsoft.com/library/windows/hardware/hh450867)枚举和驱动程序必须支持这些名称。

以下是中的新属性**KSPROPSETID\_AudioEngine**属性集：

[**KSPROPERTY\_AUDIOENGINE\_缓冲区\_大小\_范围**](https://msdn.microsoft.com/library/windows/hardware/hh450868)

[**KSPROPERTY\_AUDIOENGINE\_描述符**](https://msdn.microsoft.com/library/windows/hardware/hh450870)

[**KSPROPERTY\_AUDIOENGINE\_DEVICEFORMAT**](https://msdn.microsoft.com/library/windows/hardware/hh450872)

[**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**](https://msdn.microsoft.com/library/windows/hardware/hh450874)

[**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**](https://msdn.microsoft.com/library/windows/hardware/hh450876)

[**KSPROPERTY\_AUDIOENGINE\_LOOPBACK\_PROTECTION**](https://msdn.microsoft.com/library/windows/hardware/hh450878)

[**KSPROPERTY\_AUDIOENGINE\_MIXFORMAT**](https://msdn.microsoft.com/library/windows/hardware/hh450880)

[**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**](https://msdn.microsoft.com/library/windows/hardware/hh450884)

[**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/hh831855)

## <a name="span-idupdatestothekspropsetidaudiopropertysetspanspan-idupdatestothekspropsetidaudiopropertysetspanspan-idupdatestothekspropsetidaudiopropertysetspanupdates-to-the-kspropsetid-audio-property-set"></a><span id="Updates_to_the_KSPROPSETID__Audio_property_set"></span><span id="updates_to_the_kspropsetid__audio_property_set"></span><span id="UPDATES_TO_THE_KSPROPSETID__AUDIO_PROPERTY_SET"></span>更新到 KSPROPSETID\_音频属性集


除了支持中新的属性**KSPROPSETID\_AudioEngine**属性集，该驱动程序还必须支持中的以下现有属性[KSPROPSETID\_音频](https://msdn.microsoft.com/library/windows/hardware/ff537440)属性集：

[**KSPROPERTY\_AUDIO\_MUTE**](https://msdn.microsoft.com/library/windows/hardware/ff537293)

[**KSPROPERTY\_AUDIO\_PEAKMETER**](https://msdn.microsoft.com/library/windows/hardware/ff537296)

[**KSPROPERTY\_音频\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537309)

若要完成的硬件卸载音频处理驱动程序支持的实现，新属性已添加到并**KSPROPSETID\_音频**属性集。

以下是新**KSPROPSETID\_音频**属性：

[**KSPROPERTY\_音频\_线性\_缓冲区\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450894)

[**KSPROPERTY\_AUDIO\_PRESENTATION\_POSITION**](https://msdn.microsoft.com/library/windows/hardware/hh450895)

[**KSPROPERTY\_音频\_WAVERT\_当前\_编写\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450896)

## <a name="span-idport-classdriverupdatesandglitchreportingspanspan-idport-classdriverupdatesandglitchreportingspanspan-idport-classdriverupdatesandglitchreportingspanport-class-driver-updates-and-glitch-reporting"></a><span id="Port-class_driver_updates_and_glitch_reporting"></span><span id="port-class_driver_updates_and_glitch_reporting"></span><span id="PORT-CLASS_DRIVER_UPDATES_AND_GLITCH_REPORTING"></span>端口类驱动程序更新和故障报告


除了硬件卸载音频处理前面部分中所述的支持，Windows 端口类驱动程序还更新了与"帮助程序接口"以使其易于开发驱动程序可用于卸载音频流。 并且当这样的驱动程序检测到问题，没有一种机制，可让驱动程序报告故障错误。 以下主题提供有关的帮助程序接口和故障报告的详细信息：

[卸载音频处理的帮助程序接口](helper-interfaces-for-offloaded-audio-processing.md)

[故障报告为卸载音频](glitch-reporting-for-offloaded-audio.md)

 

 




