---
title: PROPSETID\_EXT\_传输
description: PROPSETID\_EXT\_传输
ms.assetid: 2e96dec7-43a9-44a4-9636-4ccb5244d5bd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f62a40a6bfa20f3487e7d5c52afbe751ad97bfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342167"
---
# <a name="propsetidexttransport"></a>PROPSETID\_EXT\_传输


## <span id="ddk_propsetid_ext_transport_ks"></span><span id="DDK_PROPSETID_EXT_TRANSPORT_KS"></span>


PROPSETID\_EXT\_传输属性设置控件的数据传输到和从外部设备。

KSPROPERTY\_中的 EXTXPORT 枚举*ksmedia.h*指定此集的属性。

对设置此属性是可选的仅支持外部视频捕获设备的微型驱动程序应实现的支持。

[**KSPROPERTY\_EXTXPORT\_CAPABILITIES**](ksproperty-extxport-capabilities.md)

[**KSPROPERTY\_EXTXPORT\_输入\_信号\_模式**](ksproperty-extxport-input-signal-mode.md)

[**KSPROPERTY\_EXTXPORT\_输出\_信号\_模式**](ksproperty-extxport-output-signal-mode.md)

[**KSPROPERTY\_EXTXPORT\_LOAD\_MEDIUM**](ksproperty-extxport-load-medium.md)

[**KSPROPERTY\_EXTXPORT\_MEDIUM\_INFO**](ksproperty-extxport-medium-info.md)

[**KSPROPERTY\_EXTXPORT\_STATE**](ksproperty-extxport-state.md)

[**KSPROPERTY\_EXTXPORT\_STATE\_NOTIFY**](ksproperty-extxport-state-notify.md)

[**KSPROPERTY\_EXTXPORT\_TIMECODE\_SEARCH**](ksproperty-extxport-timecode-search.md)

[**KSPROPERTY\_EXTXPORT\_ATN\_SEARCH**](ksproperty-extxport-atn-search.md)

[**KSPROPERTY\_EXTXPORT\_RTC\_SEARCH**](ksproperty-extxport-rtc-search.md)

[**KSPROPERTY\_RAW\_AVC\_CMD**](ksproperty-raw-avc-cmd.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMExtTransport**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档）。 提供对此集的属性的访问。 接口定义了许多方法，但只有外部设备控件的一部分实现。

 

 





