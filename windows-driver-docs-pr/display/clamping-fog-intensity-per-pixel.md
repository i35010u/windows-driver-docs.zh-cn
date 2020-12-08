---
title: 按像素钳接雾化强度
description: 按像素钳接雾化强度
keywords:
- 钳位雾化每像素雾化强度 DirectX 9。0
- 每像素雾化强度雾化 DirectX 9。0
- 像素雾化强度钳位 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c16979dd4d699e590b72adc75e427005cc0f838
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810307"
---
# <a name="clamping-fog-intensity-per-pixel"></a>按像素钳接雾化强度


## <span id="ddk_clamping_fog_intensity_per_pixel_gg"></span><span id="DDK_CLAMPING_FOG_INTENSITY_PER_PIXEL_GG"></span>


支持像素或顶点着色器版本2.0 及更高版本的设备的 DirectX 9.0 版本驱动程序必须通过设置 D3DPMISCCAPS FOGINFVF 功能位，来指示其设备支持钳位以每个像素为雾化强度值 \_ 。 这会通知用户在使用软件顶点着色器时，设备不会将雾化因子保存在反射 alpha 通道中。 设备可以将反射 (颜色的 alpha 通道) 到像素处理单元，而不是总是用每个顶点的雾化强度值覆盖 alpha 通道。

由于驱动程序以每像素为单位夹紧雾化强度值，因此 DirectX 9.0 和更高版本的运行时不再夹紧雾化强度值，然后将其发送到驱动程序。

驱动程序确定如何获取雾化值，具体方法是验证是否 \_ 设置了灵活顶点格式 (FVF) 中的 D3DFVF 雾化位。 如果设置了 D3DFVF \_ 雾化，驱动程序将获得按顶点传递的单独雾化值。 如果 \_ 未设置 D3DFVF 雾化并且驱动程序必须使用雾化，驱动程序将从反射颜色的 alpha 通道中获取雾化值。

当驱动程序设置 D3DPMISCCAPS \_ FOGINFVF 时，运行时将设置 \_ PrimitiveMiscCaps 结构的 **D3DCAPS9** 成员中的 D3DPMISCCAPS FOGANDSPECULARALPHA 功能位。

 

 





