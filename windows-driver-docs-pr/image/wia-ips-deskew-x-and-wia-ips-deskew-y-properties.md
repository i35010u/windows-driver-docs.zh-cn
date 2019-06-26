---
title: WIA_IPS_DESKEW_X 和 WIA_IPS_DESKEW_Y 属性
description: WIA_IPS_DESKEW_X 和 WIA_IPS_DESKEW_Y 属性
ms.assetid: 748b08f7-e838-4df8-abcb-4ff1cdd20f7e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3524f80b8c6ebeeb2641b0d6929b0c5225499006
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365477"
---
# <a name="wiaipsdeskewx-and-wiaipsdeskewy-properties"></a>WIA\_IPS\_反扭曲\_X 和 WIA\_IP\_反扭曲\_Y 属性





[ **WIA\_IPS\_反扭曲\_X** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-x)并[ **WIA\_IP\_反扭曲\_Y** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-deskew-y)属性，如果该驱动程序支持噪实现扫描程序驱动程序。 这两个属性描述中定义的边界矩形扭曲的图像的两个右上角的位置[ **WIA\_IPS\_XPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xpos)， [**WIA\_IPS\_YPOS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-ypos)， [ **WIA\_IP\_大 XEXTENT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-xextent)，和[**WIA\_IPS\_YEXTENT** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-yextent)属性。

有效值为 WIA\_IPS\_反扭曲\_X 必须是介于 0 和 (WIA\_IP\_大 XEXTENT − 1)。 有效值为 WIA\_IPS\_反扭曲\_Y 必须介于 0 和 (WIA\_IP\_YEXTENT − 1)。 值为 0，这两个属性意味着应执行任何偏斜的更正。

支持仅矩形扫描区域，因此这两个值唯一地定义要为 deskewed 的图像的位置。 可以从这两个值计算反扭曲角度。

 

 




