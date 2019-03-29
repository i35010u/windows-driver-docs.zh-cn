---
title: 顶点声明中的默认纹理坐标
description: 显示驱动程序的显示设备支持可编程像素着色器必须提供默认值的顶点声明中缺少任何纹理坐标。
ms.assetid: 5e346e7e-7460-41d9-aee1-dcc72fc642c1
keywords:
- 顶点声明 WDK DirectX 9.0
- 纹理坐标 WDK DirectX 9.0
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: caf14ee4fca311752276948be778b710fd0fc2dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568481"
---
# <a name="default-texture-coordinates-in-vertex-declarations"></a>顶点声明中的默认纹理坐标


**本主题适用于 DirectX 8.0 及更高版本。**

显示驱动程序的显示设备支持可编程像素着色器必须提供默认值的顶点声明中缺少任何纹理坐标。 向像素着色器提供的纹理坐标必须具有四个组件 （u、 v、 w，q）。 如果 u、 v 或 w 分量缺少，硬件或驱动程序必须提供默认值为 0 到该组件。 如果问题与解答组件缺少，硬件或驱动程序必须提供默认值为 1 到该组件。 因此，如果缺少的所有组件，(0,0,0,1) 是默认值。 例如，如果 2D 纹理坐标是发送到使用三维纹理坐标的像素着色器然后硬件或驱动程序提供默认值为 0 和 1 到第三和第四个组件分别。

为异常[源参数标记](https://msdn.microsoft.com/library/windows/hardware/ff569716)是使用以下指令：

`
// D3DSIO_DEF c#,f0,f1,f2,f2
`

为此指令中，源参数标记 (f\#) 作为 32 位浮点数。

 

 





