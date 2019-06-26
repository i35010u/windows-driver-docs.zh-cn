---
title: PROPSETID\_VIDCAP\_选择器
description: PROPSETID\_VIDCAP\_选择器
ms.assetid: a7328f22-be49-48ac-b923-15f66dc38ccb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3366447bd162cdefe577ccc12c4b31026cac9f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385700"
---
# <a name="propsetidvidcapselector"></a>PROPSETID\_VIDCAP\_选择器


## <span id="ddk_propsetid_vidcap_selector_ks"></span><span id="DDK_PROPSETID_VIDCAP_SELECTOR_KS"></span>


PROPSETID\_VIDCAP\_选择器属性集是用于新[USB 视频类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)。 设置此属性包含实现所需的属性**ISelector**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档）。

KSPROPERTY\_VIDCAP\_中的选择器枚举*ksmedia.h*指定此集的属性。

此属性设置控件当前正在提供可重用功能区输入的节点。 支持设置此属性是可选的应仅由设备提供这些控件的实现。

USB 视频类驱动程序的客户端可以发出以下请求的筛选器或节点：

[**KSPROPERTY\_选择器\_源\_节点\_ID**](ksproperty-selector-source-node-id.md)

[**KSPROPERTY\_NUM\_源**](ksproperty-num-sources.md)

### <a name="span-iddirectshowinterfacesspanspan-iddirectshowinterfacesspandirectshow-interfaces"></a><span id="directshow_interfaces"></span><span id="DIRECTSHOW_INTERFACES"></span>DirectShow 接口

属性在 PROPSETID\_VIDCAP\_选择器属性集访问通过 DirectShow **ISelector**接口 （请参阅 Microsoft Windows SDK 中的 DirectShow 文档）。

 

 





