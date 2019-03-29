---
title: PROPSETID\_VIDCAP\_CROSSBAR
description: PROPSETID\_VIDCAP\_CROSSBAR
ms.assetid: a2ed126c-75ee-4346-845e-9f675ca34416
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7549c59fae62b8a0af905aa2ccce1244a23eac8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561517"
---
# <a name="propsetidvidcapcrossbar"></a>PROPSETID\_VIDCAP\_CROSSBAR


## <span id="ddk_propsetid_vidcap_crossbar_ks"></span><span id="DDK_PROPSETID_VIDCAP_CROSSBAR_KS"></span>


PROPSETID\_VIDCAP\_纵横制属性设置控件路由视频和音频信号的设备。 上一个常规的切换矩阵，其中 N 输入和 M 输出建模纵横制。 输入任何的信号可路由到一个或多个输出，尽管实际的硬件实现可能会允许此常规路由功能的一个子集。 十字条可用于路由数字或模拟信号。 单个纵横制可以路由视频和音频信号。 （可选） 视频插针可指示到视频插针相关的音频 pin。

KSPROPERTY\_VIDCAP\_中的十字条枚举*ksmedia.h*指定此集的属性。

支持设置此属性是可选的应仅由十字条设备的微型驱动程序实现。

纵横制捕获微型驱动程序需要实现以下属性：

[**KSPROPERTY\_CROSSBAR\_CAN\_ROUTE**](ksproperty-crossbar-can-route.md)

[**KSPROPERTY\_CROSSBAR\_CAPS**](ksproperty-crossbar-caps.md)

[**KSPROPERTY\_CROSSBAR\_PININFO**](ksproperty-crossbar-pininfo.md)

[**KSPROPERTY\_CROSSBAR\_ROUTE**](ksproperty-crossbar-route.md)

### <a name="span-iddirectshowinterfacespanspan-iddirectshowinterfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMCrossbar**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档） 提供对此集的属性的访问。

 

 





