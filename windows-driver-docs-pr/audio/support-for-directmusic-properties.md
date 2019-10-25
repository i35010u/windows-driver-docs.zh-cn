---
title: 对 DirectMusic 属性的支持
description: 对 DirectMusic 属性的支持
ms.assetid: f44cf9a9-bdfc-4794-b064-4d1126fb83aa
keywords:
- 硬件加速 WDK 音频
- 微型端口驱动程序 WDK 音频、内核模式硬件加速
- 合成 WDK 音频，内核模式硬件加速
- 合成 WDK 音频，属性支持
- IKsControl 接口
- 属性集 Guid WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79eedcd1d98a356d89aa1a6412bd0bdf6b17a801
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832349"
---
# <a name="support-for-directmusic-properties"></a>对 DirectMusic 属性的支持


## <span id="support_for_directmusic_properties"></span><span id="SUPPORT_FOR_DIRECTMUSIC_PROPERTIES"></span>


DirectMusic 合成微型端口驱动程序以属性项数组的形式指定其硬件功能。 每个属性项都是一个[**PCPROPERTY\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item)结构，其中包含以下内容：

-   定义由 DirectMusic 定义的特定硬件功能的属性集 GUID。

-   指向在驱动程序中实现的属性处理程序方法的指针。

-   一组标志，用于指定处理程序是否可以获取属性、设置属性并指示对属性的基本支持。

### <a name="span-idproperty_set_guidsspanspan-idproperty_set_guidsspanproperty-set-guids"></a><span id="property_set_guids"></span><span id="PROPERTY_SET_GUIDS"></span>属性集 Guid

DirectMusic 定义了以下属性集 Guid：

-   GUID\_DMU\_\_DLS1

-   GUID\_DMU\_\_DLS2

-   GUID\_DMU\_的\_效果

-   GUID\_DMU\_\_GM\_硬件

-   GUID\_DMU\_功能\_GS\_支持

-   GUID\_DMU\_的\_GS\_硬件

-   GUID\_DMU\_\_INSTRUMENT2

-   GUID\_DMU\_\_LegacyCaps

-   GUID\_DMU\_\_MemorySize

-   GUID\_DMU\_\_SampleMemorySize

-   GUID\_DMU\_\_SamplePlaybackRate

-   GUID\_DMU\_\_SetSynthSink

-   GUID\_DMU\_\_SynthSink\_DSOUND

-   GUID\_DMU\_\_SynthSink\_波

-   GUID\_DMU\_的\_卷

-   GUID\_DMU\_\_WavesReverb

-   GUID\_DMU\_\_WriteLatency

-   GUID\_DMU\_\_WritePeriod

-   GUID\_DMU\_支持\_XG\_

-   GUID\_DMU\_\_XG\_硬件

有关上述属性集 Guid 的定义，请参阅 Microsoft Windows SDK 中 DirectX 8.0 程序员参考中的[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))结构说明。 为上述每个 Guid 设置的属性包含一个元素，该元素由零的索引标识。

### <a name="span-idikscontrol_interfacespanspan-idikscontrol_interfacespanikscontrol-interface"></a><span id="ikscontrol_interface"></span><span id="IKSCONTROL_INTERFACE"></span>IKsControl 接口

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)接口用于获取、设置或查询属性、事件和方法的基本支持。 此接口是 WDM 内核流式处理（KS）体系结构的一部分，但 DirectMusic 也使用它来公开 DirectMusic 端口的属性。 若要检索此接口，请调用**IDirectMusicPort：： QueryInterface**方法（如 Windows SDK 文档中所述），将*riid*参数设置为**IID\_IKsControl**。

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)接口有三种方法： [**KsProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksproperty)、 [**KsEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksevent)和[**KsMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksmethod)。 目前，DirectMusic 只支持**KsProperty** 。

[**IKsControl：： KsProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ikscontrol-ksproperty)方法获取或设置属性的值。 将属性项请求路由到特定 DirectMusic 端口的方式取决于端口的实现方式：

-   在基于 Microsoft Win32 处理程序的多媒体调用（midiOut 和 midiIn Api）上，表示 DirectMusic 仿真的端口不支持任何属性。 使用**GUID\_dmu\_属性\_LegacyCaps**属性集 GUID 来查询端口是否是使用 Win32 多媒体调用来实现的。

-   对表示可插接式软件合成器的端口的属性项请求将完全在用户模式下处理。 此类端口的拓扑是连接到接收器节点（ [IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)接口）的合成器（由[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)接口表示）。 首先向合成器节点提供属性请求，然后将其提供给 "接收器" 节点（如果它无法被合成器识别）。

 

 




