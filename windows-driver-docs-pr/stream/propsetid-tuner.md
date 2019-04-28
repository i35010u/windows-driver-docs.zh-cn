---
title: PROPSETID\_调谐器
description: PROPSETID\_调谐器
ms.assetid: 2697fb71-32da-40d0-aebf-d91b1a0587ba
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66be9e3183620e9bee2011e23eae0877db773abb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342149"
---
# <a name="propsetidtuner"></a>PROPSETID\_调谐器


## <span id="ddk_propsetid_tuner_ks"></span><span id="DDK_PROPSETID_TUNER_KS"></span>


PROPSETID\_调谐器属性设置控件的设备，该支持电视或广播优化。 此属性设置为 multistandard 视频调谐器，以及具有多个输入的调谐器提供支持。

KSPROPERTY\_中的调谐器枚举*ksmedia.h*指定此集的属性。

对设置此属性是可选的仅支持电视或广播优化的微型驱动程序应实现的支持。

调谐器捕获微型驱动程序需要实现以下属性：

[**KSPROPERTY\_调谐器\_CAP**](ksproperty-tuner-caps.md)

[**KSPROPERTY\_调谐器\_频率**](ksproperty-tuner-frequency.md)

[**KSPROPERTY\_调谐器\_输入**](ksproperty-tuner-input.md)

[**KSPROPERTY\_调谐器\_模式**](ksproperty-tuner-mode.md)

[**KSPROPERTY\_调谐器\_模式\_CAP**](ksproperty-tuner-mode-caps.md)

[**KSPROPERTY\_调谐器\_扫描\_CAP** ](ksproperty-tuner-scan-caps.md) Windows Vista 的新增功能

[**KSPROPERTY\_调谐器\_标准**](ksproperty-tuner-standard.md)

[**KSPROPERTY\_调谐器\_状态**](ksproperty-tuner-status.md)

调谐器捕获微型驱动程序可以选择实现以下属性：

[**KSPROPERTY\_TUNER\_IF\_MEDIUM**](ksproperty-tuner-if-medium.md)

[**KSPROPERTY\_调谐器\_NETWORKTYPE\_扫描\_CAPS** ](ksproperty-tuner-networktype-scan-caps.md) Windows Vista 的新增功能

[**KSPROPERTY\_调谐器\_扫描\_状态**](ksproperty-tuner-scan-status.md) Windows Vista 的新增功能

[**KSPROPERTY\_调谐器\_标准\_模式**](ksproperty-tuner-standard-mode.md) Windows Vista 的新增功能

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMTVTuner**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档） 提供对此集的属性的访问。

 

 





