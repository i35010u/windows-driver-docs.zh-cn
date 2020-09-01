---
title: WIA_IPS_DESKEW_X 和 WIA_IPS_DESKEW_Y 属性
description: WIA_IPS_DESKEW_X 和 WIA_IPS_DESKEW_Y 属性
ms.assetid: 748b08f7-e838-4df8-abcb-4ff1cdd20f7e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 767a19508f63b1132927ca5d8f227466f3f7b5de
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191683"
---
# <a name="wia_ips_deskew_x-and-wia_ips_deskew_y-properties"></a>WIA \_ ip \_ 反扭曲 \_ X 和 WIA \_ Ip \_ 反扭曲 \_ Y 属性





如果驱动程序支持 deskewing， [**wia \_ ip \_ 反扭曲 \_ X**](./wia-ips-deskew-x.md) 和 [**wia \_ ip \_ 抗扭反的 \_ Y**](./wia-ips-deskew-y.md) 属性由 scanner 驱动程序实现。 这两个属性说明了在 [**wia \_ ip \_ XPOS**](./wia-ips-xpos.md)、 [**wia \_ ip \_ YPOS**](./wia-ips-ypos.md)、 [**wia \_ ips \_ XEXTENT**](./wia-ips-xextent.md)和 [**wia \_ ip \_ YEXTENT**](./wia-ips-yextent.md) 属性定义的边框内，倾斜图像的两个顶角所在的位置。

WIA \_ ip \_ 反扭曲 X 的有效值值 \_ 必须介于0和 (WIA \_ ip \_ XEXTENT − 1) 之间。 WIA \_ ip \_ 反扭曲 Y 的有效值 \_ 必须介于0和 (WIA \_ ip \_ YEXTENT − 1) 之间。 如果这两个属性的值为0，则表示不应执行任何歪斜更正。

仅支持矩形扫描区域，因此，这两个值可唯一定义要 deskewed 的图像的位置。 可以从这两个值计算反扭曲角。

 

