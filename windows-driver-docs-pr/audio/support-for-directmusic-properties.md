---
title: 对 DirectMusic 属性的支持
description: 对 DirectMusic 属性的支持
ms.assetid: f44cf9a9-bdfc-4794-b064-4d1126fb83aa
keywords:
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频，内核模式硬件加速
- 合成器 WDK 音频，内核模式硬件加速
- 合成器 WDK 音频，属性支持
- IKsControl 接口
- 属性集 Guid WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 854c1a876db2cd3f71fc8582558d3dc9b69c3e20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354244"
---
# <a name="support-for-directmusic-properties"></a>对 DirectMusic 属性的支持


## <span id="support_for_directmusic_properties"></span><span id="SUPPORT_FOR_DIRECTMUSIC_PROPERTIES"></span>


DirectMusic 合成微型端口驱动程序中属性项的数组的形式指定其硬件功能。 每个属性项是[ **PCPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcproperty_item)包含以下结构：

-   属性集 GUID，用于定义由 DirectMusic 定义特定的硬件功能。

-   指向在驱动程序中实现的属性处理程序方法的指针。

-   一组标志，用于指定该处理程序可以获取其属性、 设置属性，并指示对该属性的基本支持。

### <a name="span-idpropertysetguidsspanspan-idpropertysetguidsspanproperty-set-guids"></a><span id="property_set_guids"></span><span id="PROPERTY_SET_GUIDS"></span>属性集 Guid

DirectMusic 定义以下属性集 Guid:

-   GUID\_DMUS\_PROP\_DLS1

-   GUID\_DMU\_PROP\_DLS2

-   GUID\_DMUS\_PROP\_Effects

-   GUID\_DMUS\_PROP\_GM\_Hardware

-   GUID\_DMUS\_PROP\_GS\_Capable

-   GUID\_DMUS\_PROP\_GS\_Hardware

-   GUID\_DMUS\_PROP\_INSTRUMENT2

-   GUID\_DMUS\_PROP\_LegacyCaps

-   GUID\_DMUS\_PROP\_MemorySize

-   GUID\_DMUS\_PROP\_SampleMemorySize

-   GUID\_DMUS\_PROP\_SamplePlaybackRate

-   GUID\_DMUS\_PROP\_SetSynthSink

-   GUID\_DMUS\_PROP\_SynthSink\_DSOUND

-   GUID\_DMUS\_PROP\_SynthSink\_WAVE

-   GUID\_DMU\_PROP\_卷

-   GUID\_DMUS\_PROP\_WavesReverb

-   GUID\_DMUS\_PROP\_WriteLatency

-   GUID\_DMUS\_PROP\_WritePeriod

-   GUID\_DMUS\_PROP\_XG\_Capable

-   GUID\_DMU\_PROP\_XG\_硬件

有关定义上述属性集 Guid，请参阅的说明[ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)) Microsoft Windows SDK 中的 DirectX 8.0 程序员参考中的结构。 将属性设置为每个前面的 Guid 包含的零索引标识的单个元素。

### <a name="span-idikscontrolinterfacespanspan-idikscontrolinterfacespanikscontrol-interface"></a><span id="ikscontrol_interface"></span><span id="IKSCONTROL_INTERFACE"></span>IKsControl 接口

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol)接口用于获取、 设置或查询的基本支持的属性、 事件和方法。 此接口是 WDM 内核流式处理 (KS) 体系结构的一部分，但还用于通过 DirectMusic 公开 DirectMusic 端口的属性。 若要检索此接口，请调用**IDirectMusicPort::QueryInterface**方法 （Windows SDK 文档中所述），替换*riid*参数设置为**IID\_IKsControl**。

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol)接口有三个方法：[**KsProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksproperty)， [ **KsEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksevent)，以及[ **KsMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksmethod)。 目前，仅**KsProperty** DirectMusic 支持。

[ **IKsControl::KsProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ikscontrol-ksproperty)方法获取或设置属性的值。 中的属性项请求路由到特定的 DirectMusic 端口的方式取决于该端口如何实现：

-   表示基于 Microsoft Win32 句柄基于多媒体调用 （midiOut 和 midiIn Api） DirectMusic 仿真的端口不支持任何属性。 使用**GUID\_DMU\_PROP\_LegacyCaps**属性集 GUID 来查询它实现与 Win32 多媒体调用的端口。

-   表示可插拔软件合成器的端口的属性项请求完全在用户模式下处理。 此类型的端口的拓扑是合成器 (由[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)接口) 连接到汇聚节点 ( [IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)接口)。 属性请求都在第一次合成器节点，然后写入接收器节点如果合成器无法识别。

 

 




