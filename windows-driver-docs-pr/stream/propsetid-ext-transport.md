---
title: PROPSETID \_ 扩展 \_ 传输
description: PROPSETID \_ 扩展 \_ 传输
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60c2ed79ea2560ffccd1402d43c66a531793ba98
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783727"
---
# <a name="propsetid_ext_transport"></a>PROPSETID \_ 扩展 \_ 传输


## <span id="ddk_propsetid_ext_transport_ks"></span><span id="DDK_PROPSETID_EXT_TRANSPORT_KS"></span>


PROPSETID \_ 扩展 \_ 传输属性集控制数据与外部设备之间的传输。

\_ *Ksmedia* 中的 KSPROPERTY EXTXPORT 枚举指定此集的属性。

对此属性集的支持是可选的，只应由支持外部视频捕获设备的微型驱动程序实现。

[**KSPROPERTY \_ EXTXPORT \_ 功能**](ksproperty-extxport-capabilities.md)

[**KSPROPERTY \_ EXTXPORT \_ 输入 \_ 信号 \_ 模式**](ksproperty-extxport-input-signal-mode.md)

[**KSPROPERTY \_ EXTXPORT \_ 输出 \_ 信号 \_ 模式**](ksproperty-extxport-output-signal-mode.md)

[**KSPROPERTY \_ EXTXPORT \_ LOAD \_ MEDIUM**](ksproperty-extxport-load-medium.md)

[**KSPROPERTY \_ EXTXPORT \_ 中型 \_ 信息**](ksproperty-extxport-medium-info.md)

[**KSPROPERTY \_ EXTXPORT \_ 状态**](ksproperty-extxport-state.md)

[**KSPROPERTY \_ EXTXPORT \_ 状态 \_ 通知**](ksproperty-extxport-state-notify.md)

[**KSPROPERTY \_ EXTXPORT 时间 \_ 码 \_ 搜索**](ksproperty-extxport-timecode-search.md)

[**KSPROPERTY \_ EXTXPORT \_ ATN \_ 搜索**](ksproperty-extxport-atn-search.md)

[**KSPROPERTY \_ EXTXPORT \_ RTC \_ 搜索**](ksproperty-extxport-rtc-search.md)

[**KSPROPERTY \_ RAW \_ AVC \_ CMD**](ksproperty-raw-avc-cmd.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMExtTransport** 接口 (参阅 Microsoft Windows SDK) 中的 directshow 文档。 提供对此集的属性的访问。 接口定义了许多方法，但仅实现了外部设备控件的子集。

 

 





