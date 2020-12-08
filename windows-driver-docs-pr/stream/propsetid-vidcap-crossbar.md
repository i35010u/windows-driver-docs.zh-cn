---
title: PROPSETID \_ VIDCAP \_ 横线
description: PROPSETID \_ VIDCAP \_ 横线
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eac10a096017091dc9c59fea27e00457b61f7fa0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833953"
---
# <a name="propsetid_vidcap_crossbar"></a>PROPSETID \_ VIDCAP \_ 横线


## <span id="ddk_propsetid_vidcap_crossbar_ks"></span><span id="DDK_PROPSETID_VIDCAP_CROSSBAR_KS"></span>


PROPSETID \_ VIDCAP \_ 纵横比属性集控制路由视频和音频信号的设备。 该纵横比在具有 N 个输入和 M 个输出的常规切换矩阵上建模。 可以将任何输入信号路由到一个或多个输出，但实际的硬件实现可能只允许使用此常规路由功能的一个子集。 可以使用纵横制来路由数字或模拟信号。 单个纵横条可以路由视频和音频信号。 视频 pin （可选）可以指示与视频 pin 相关的音频 pin。

\_Ksmedia 中的 KSPROPERTY VIDCAP \_ 纵横 *ksmedia.h* 数枚举指定此集的属性。

对此属性集的支持是可选的，并且应仅由纵横比的微型驱动程序设备来实现。

要实现以下属性，需要执行纵横制捕获微型驱动程序：

[**KSPROPERTY \_ 横线 \_ 可以 \_ 路由**](ksproperty-crossbar-can-route.md)

[**KSPROPERTY \_ 横线 \_ 帽**](ksproperty-crossbar-caps.md)

[**KSPROPERTY \_ 横线 \_ PININFO**](ksproperty-crossbar-pininfo.md)

[**KSPROPERTY \_ 横线 \_ 路由**](ksproperty-crossbar-route.md)

### <a name="span-iddirectshow_interfacespanspan-iddirectshow_interfacespandirectshow-interface"></a><span id="directshow_interface"></span><span id="DIRECTSHOW_INTERFACE"></span>DirectShow 接口

DirectShow **IAMCrossbar** 接口 (参阅 Microsoft Windows SDK 中的 directshow 文档) 提供对此集的属性的访问权限。

 

 





