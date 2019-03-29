---
title: PROPSETID\_VIDCAP\_TVAUDIO
description: PROPSETID\_VIDCAP\_TVAUDIO
ms.assetid: 33c76f30-2e4b-48b7-a463-f6363419dca3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35eba440585299c5e9a26b1c28b142cf9e9d3455
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576314"
---
# <a name="propsetidvidcaptvaudio"></a>PROPSETID\_VIDCAP\_TVAUDIO


## <span id="ddk_propsetid_vidcap_tvaudio_ks"></span><span id="DDK_PROPSETID_VIDCAP_TVAUDIO_KS"></span>


PROPSETID\_VIDCAP\_TVAUDIO 属性设置是唯一的音频与电视源相关联的控件设置。 这包括辅助音频程序 (SAP) 和立体声或 mono 选择。 这些控件通常位于设备上的外部系统音频混音器。

KSPROPERTY\_VIDCAP\_中的 TVAUDIO 枚举*ksmedia.h*指定此集的属性。

对设置此属性是可选的仅支持电视音频的设备的微型驱动程序应实现的支持。

电视音频捕获微型驱动程序需要实现以下属性：

[**KSPROPERTY\_TVAUDIO\_CAPS**](ksproperty-tvaudio-caps.md)

[**KSPROPERTY\_TVAUDIO\_目前\_可用\_模式**](ksproperty-tvaudio-currently-available-modes.md)

[**KSPROPERTY\_TVAUDIO\_模式**](ksproperty-tvaudio-mode.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMTVAudio**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档） 提供对此集的属性的访问。

 

 





