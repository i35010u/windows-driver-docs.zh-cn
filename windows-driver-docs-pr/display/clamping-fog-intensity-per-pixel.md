---
title: 按像素钳接雾化强度
description: 按像素钳接雾化强度
ms.assetid: 249d085a-b54c-48b3-bc7a-3fe5f8238b1b
keywords:
- 每个像素 WDK DirectX 9.0 夹紧雾强度
- 每个像素 WDK DirectX 9.0 雾强度
- 固定 WDK DirectX 9.0 像素雾强度
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfbd86db9c30804eb9cf9b48fb0cb42eaee09aa9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354329"
---
# <a name="clamping-fog-intensity-per-pixel"></a>按像素钳接雾化强度


## <span id="ddk_clamping_fog_intensity_per_pixel_gg"></span><span id="DDK_CLAMPING_FOG_INTENSITY_PER_PIXEL_GG"></span>


支持像素或顶点着色器版本 2.0 及更高版本的设备的 DirectX 9.0 版本驱动程序必须指明其设备支持固定雾强度值在每个像素的基础上通过设置 D3DPMISCCAPS\_FOGINFVF 功能位。 这会通知用户，设备不会保存雾身份中的反射高光的 alpha 通道时使用软件顶点着色器。 设备可以向像素处理单元，而不是始终使用每个顶点雾强度值覆盖 alpha 通道传递 （fixed 的函数顶点管道中计算） 的反射颜色的 alpha 通道。

该驱动程序在每个像素的基础上固定雾强度值，因为运行时的 DirectX 9.0 和更高版本不能再发送到该驱动程序之前固定雾明暗度值。

该驱动程序确定如何获取雾值通过验证如果 D3DFVF\_雾灵活顶点格式 (FVF) 中的位设置。 如果 D3DFVF\_雾设置、 驱动程序将获取每顶点传递的单独雾值。 如果 D3DFVF\_雾未设置和驱动程序必须使用雾，驱动程序将从反射颜色的 alpha 通道获取雾值。

当驱动程序设置 D3DPMISCCAPS\_FOGINFVF，运行时又设置 D3DPMISCCAPS\_FOGANDSPECULARALPHA 功能位**PrimitiveMiscCaps** D3DCAPS9 结构中的成员。

 

 





