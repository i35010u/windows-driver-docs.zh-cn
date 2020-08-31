---
title: 顶点声明中的默认纹理坐标
description: 显示设备支持可编程像素着色器的显示驱动程序必须为顶点声明中缺少的任何纹理坐标提供默认值。
ms.assetid: 5e346e7e-7460-41d9-aee1-dcc72fc642c1
keywords:
- 顶点声明 WDK DirectX 9。0
- 纹理协调 WDK DirectX 9。0
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 684a943e151b63e482433fe9b06cf4b9370d1e53
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064008"
---
# <a name="default-texture-coordinates-in-vertex-declarations"></a>顶点声明中的默认纹理坐标


**本主题适用于 DirectX 8.0 和更高版本。**

显示设备支持可编程像素着色器的显示驱动程序必须为顶点声明中缺少的任何纹理坐标提供默认值。 提供给像素着色器的纹理坐标必须具有四个组件 (u、v、w、q) 。 如果缺少 u、v 或 w 组件，则硬件或驱动程序必须将默认值0提供给该组件。 如果缺少 q 组件，则硬件或驱动程序必须将默认值1提供给该组件。 因此，如果所有组件都丢失， (0，0，0，1) 为默认值。 例如，如果将二维纹理坐标发送到使用三维纹理坐标的像素着色器，则硬件或驱动程序将分别向第三个和第四个组件提供默认值0和1。

[源参数标记](./source-parameter-token.md)的例外情况如下：

`
// D3DSIO_DEF c#,f0,f1,f2,f2
`

对于此说明，将 (f) 的源参数标记 \# 取为32位浮点。

 

