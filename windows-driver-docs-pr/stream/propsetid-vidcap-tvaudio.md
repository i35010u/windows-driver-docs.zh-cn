---
title: PROPSETID \_ VIDCAP \_ TVAUDIO
description: PROPSETID \_ VIDCAP \_ TVAUDIO
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc6110d8f97a1af9e3f92d3a926a9ec3d0b69e13
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840509"
---
# <a name="propsetid_vidcap_tvaudio"></a>PROPSETID \_ VIDCAP \_ TVAUDIO


## <span id="ddk_propsetid_vidcap_tvaudio_ks"></span><span id="DDK_PROPSETID_VIDCAP_TVAUDIO_KS"></span>


PROPSETID \_ VIDCAP \_ TVAUDIO 属性集控制与电视源关联的音频的设置。 这包括 (SAP) 的辅助音频程序以及立体声或 mono 选择。 通常，这些控件位于系统音频混音器外部的设备上。

\_Ksmedia 中的 KSPROPERTY VIDCAP \_ TVAUDIO *ksmedia.h* 枚举指定此集的属性。

对此属性集的支持是可选的，只应由支持电视音频的设备微型驱动程序实现。

需要 TV 音频捕获微型驱动程序来实现以下属性：

[**KSPROPERTY \_ TVAUDIO \_ CAP**](ksproperty-tvaudio-caps.md)

[**KSPROPERTY \_ TVAUDIO \_ 当前 \_ 可用 \_ 模式**](ksproperty-tvaudio-currently-available-modes.md)

[**KSPROPERTY \_ TVAUDIO \_ 模式**](ksproperty-tvaudio-mode.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMTVAudio** 接口 (参阅 Microsoft Windows SDK 中的 directshow 文档) 提供对此集的属性的访问权限。

 

 





