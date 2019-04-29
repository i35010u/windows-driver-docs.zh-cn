---
title: 顶点和像素雾化
description: 顶点和像素雾化
ms.assetid: 4cdba82f-0cfe-4416-951c-59b577c7f30e
keywords:
- 雾化 WDK Direct3D 像素
- 顶点雾 WDK Direct3D
- 雾化 WDK Direct3D
- 线性雾 WDK Direct3D
- 指数雾 WDK Direct3D
- 指数平方的雾 WDK Direct3D
- 单色照明 WDK Direct3D
- 颜色雾计算 WDK Direct3D
- 混合雾身份 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f6cb7e11cbc1802167deb8881fe0b9e2a06e4c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390787"
---
# <a name="vertex-and-pixel-fogging"></a>顶点和像素雾化


## <span id="ddk_vertex_and_pixel_fogging_gg"></span><span id="DDK_VERTEX_AND_PIXEL_FOGGING_GG"></span>


雾有三个主要配置文件类型： 线性、 指数函数和指数平方值。 此外，还有两个主要的实现方法： 顶点雾 （也称为迭代或本地模糊） 和像素雾 （也称为表或全局雾）。

在单色 （冲刺） 照明模式下，雾可以仅当雾颜色为黑色时正常工作。 （如果有任何照明，任何雾颜色有效因为雾呈现为黑色。）可以是雾视为对象的可见性-雾值越低、 更高版本的模糊效果和不可见的度量值。

混合身份雾**f**所有雾计算中使用。 它代表的对象的颜色与雾颜色比例。 最终颜色由以下公式确定：

**颜色 = f \* objColor + (1.0-f) \* fogColor**

因此，混合身份 0.0 一团迷雾是完整雾颜色和混合因子 1.0 一团迷雾是完整的对象的颜色。 通常情况下， **f**与距离会降低。

下图所示，线性雾密度以线性方式增加，随着距离的增加。

![说明线性雾的关系图](images/d3dfig23.png)

此线性增加不同于指数雾雾密度以指数方式增加。 可以按如下所示设置线性雾配置文件： D3DRENDERSTATE\_FOGSTART 呈现状态设置为 ZFront 并*f* = 1.0; D3DRENDERSTATE\_FOGEND 呈现状态设置为 ZBack 和*f* = 0.0。 D3DRENDERSTATE\_FOGDENSITY 呈现状态将被忽略。

 

 





