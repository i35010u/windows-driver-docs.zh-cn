---
title: 对 DirectMusic 属性的支持
description: 对 DirectMusic 属性的支持
keywords:
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频、内核模式硬件加速
- 合成 WDK 音频，内核模式硬件加速
- 合成 WDK 音频，属性支持
- IKsControl 接口
- 属性集 Guid WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0b4091446364ec723a05e1503f41029f767ef4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800589"
---
# <a name="support-for-directmusic-properties"></a>对 DirectMusic 属性的支持


## <span id="support_for_directmusic_properties"></span><span id="SUPPORT_FOR_DIRECTMUSIC_PROPERTIES"></span>


DirectMusic 合成微型端口驱动程序以属性项数组的形式指定其硬件功能。 每个属性项都是一个 [**PCPROPERTY \_ 项**](/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item) 结构，其中包含以下内容：

-   定义由 DirectMusic 定义的特定硬件功能的属性集 GUID。

-   指向在驱动程序中实现的属性处理程序方法的指针。

-   一组标志，用于指定处理程序是否可以获取属性、设置属性并指示对属性的基本支持。

### <a name="span-idproperty_set_guidsspanspan-idproperty_set_guidsspanproperty-set-guids"></a><span id="property_set_guids"></span><span id="PROPERTY_SET_GUIDS"></span>属性集 Guid

DirectMusic 定义了以下属性集 Guid：

-   GUID \_ dmu \_ \_ DLS1

-   GUID \_ dmu \_ \_ DLS2

-   GUID \_ dmu \_ 的 \_ 结果

-   GUID \_ dmu \_ \_ 通用 \_ 硬件

-   GUID \_ dmu \_ \_ 支持的 \_ 支持 GS

-   GUID \_ dmu \_ 将 \_ GS \_ 硬件

-   GUID \_ dmu \_ \_ INSTRUMENT2

-   GUID \_ dmu \_ \_ LegacyCaps

-   GUID \_ dmu \_ \_ MemorySize

-   GUID \_ dmu \_ \_ SampleMemorySize

-   GUID \_ dmu \_ \_ SamplePlaybackRate

-   GUID \_ dmu \_ \_ SetSynthSink

-   GUID \_ dmu \_ \_ SynthSink \_ DSOUND

-   GUID \_ dmu \_ \_ SynthSink \_ WAVE

-   GUID \_ dmu \_ 的 \_ 数量

-   GUID \_ dmu \_ \_ WavesReverb

-   GUID \_ dmu \_ \_ WriteLatency

-   GUID \_ dmu \_ \_ WritePeriod

-   GUID \_ dmu \_ \_ 支持 XG \_

-   GUID \_ dmu \_ \_ XG \_ 硬件

有关上述属性集 Guid 的定义，请参阅 Microsoft Windows SDK 中 DirectX 8.0 程序员参考中的 [**KSPROPERTY**](/previous-versions/ff564262(v=vs.85)) 结构说明。 为上述每个 Guid 设置的属性包含一个元素，该元素由零的索引标识。

### <a name="span-idikscontrol_interfacespanspan-idikscontrol_interfacespanikscontrol-interface"></a><span id="ikscontrol_interface"></span><span id="IKSCONTROL_INTERFACE"></span>IKsControl 接口

[IKsControl](/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)接口用于获取、设置或查询属性、事件和方法的基本支持。 此接口是 WDM 内核流式传输 (KS) 体系结构的一部分，但 DirectMusic 也使用它来公开 DirectMusic 端口的属性。 若要检索此接口，请调用 Windows SDK 文档) 中所述的 **IDirectMusicPort：： QueryInterface** (方法，其中 *riid* 参数设置为 **\_ IKsControl**。

[IKsControl](/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)接口有三种方法： [**KsProperty**](/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksproperty)、 [**KsEvent**](/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksevent)和 [**KsMethod**](/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksmethod)。 目前，DirectMusic 只支持 **KsProperty** 。

[**IKsControl：： KsProperty**](/windows-hardware/drivers/ddi/ks/nf-ks-ikscontrol-ksproperty)方法获取或设置属性的值。 将属性项请求路由到特定 DirectMusic 端口的方式取决于端口的实现方式：

-   在 midiOut 和 midiIn Api)  (基于 Microsoft Win32 基于句柄的多媒体调用的端口不支持任何属性。 使用 **guid \_ dmu \_ \_** 属性集 guid 查询端口是否是使用 Win32 多媒体调用来实现的。

-   对表示可插接式软件合成器的端口的属性项请求将完全在用户模式下处理。 这种类型的端口的拓扑 [是一种](/windows/win32/api/dmusics/nn-dmusics-idirectmusicsynth) 合成器 (，) 连接到接收器节点 ([IDirectMusicSynthSink](/windows/win32/api/dmusics/nn-dmusics-idirectmusicsynthsink) 接口) 。 首先向合成器节点提供属性请求，然后将其提供给 "接收器" 节点（如果它无法被合成器识别）。

 

