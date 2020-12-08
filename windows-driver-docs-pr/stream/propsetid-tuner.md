---
title: PROPSETID \_ 调谐器
description: PROPSETID \_ 调谐器
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf5e89ec3c8ab8d3240db3205dd77ebf5d1f7a7b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811329"
---
# <a name="propsetid_tuner"></a>PROPSETID \_ 调谐器


## <span id="ddk_propsetid_tuner_ks"></span><span id="DDK_PROPSETID_TUNER_KS"></span>


PROPSETID \_ 调谐器属性集控制支持电视或收音机调谐的设备。 此属性集为 multistandard 视频调谐器以及包含多个输入的调谐器提供支持。

\_ *Ksmedia* 中的 KSPROPERTY 调谐器枚举指定此集的属性。

对此属性集的支持是可选的，只应由支持电视或无线电优化的微型驱动程序实现。

需要调谐器捕获微型驱动程序来实现以下属性：

[**KSPROPERTY \_ 调谐器 \_ CAP**](ksproperty-tuner-caps.md)

[**KSPROPERTY \_ 调谐器 \_ 频率**](ksproperty-tuner-frequency.md)

[**KSPROPERTY \_ 调谐器 \_ 输入**](ksproperty-tuner-input.md)

[**KSPROPERTY \_ 调谐器 \_ 模式**](ksproperty-tuner-mode.md)

[**KSPROPERTY \_ 调谐器 \_ 模式 \_ CAP**](ksproperty-tuner-mode-caps.md)

[**KSPROPERTY \_适用于 Windows Vista 的调谐器 \_ 扫描 \_ cap**](ksproperty-tuner-scan-caps.md) 新增

[**KSPROPERTY \_ 调谐器 \_ 标准版**](ksproperty-tuner-standard.md)

[**KSPROPERTY \_ 调谐器 \_ 状态**](ksproperty-tuner-status.md)

调谐器捕获微型驱动程序可以选择实现以下属性：

[**KSPROPERTY \_ 调谐器 \_ IF \_ 中型**](ksproperty-tuner-if-medium.md)

[**KSPROPERTY \_适用于 Windows Vista 的调谐器 \_ NETWORKTYPE \_ 扫描 \_ cap**](ksproperty-tuner-networktype-scan-caps.md) 新增

[**KSPROPERTY \_Windows Vista 的调谐器 \_ 扫描 \_ 状态**](ksproperty-tuner-scan-status.md) 新增

[**KSPROPERTY \_适用于 Windows Vista 的调谐器 \_ 标准 \_ 模式**](ksproperty-tuner-standard-mode.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMTVTuner** 接口 (参阅 Microsoft Windows SDK 中的 directshow 文档) 提供对此集的属性的访问权限。

 

 





