---
title: 光栅器块
description: 光栅器块
ms.assetid: 115c265d-0264-4a8a-b07b-710438394c68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08364909ef7f3bd3075ef83b04314e5e5d377b24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372984"
---
# <a name="rasterizer-block"></a>光栅器块


光栅器块剪辑、 设置基元，并确定如何调用像素着色器阶段。 Direct3D 运行时不会不查看管道中阶段的光栅器块。 相反，Direct3D 运行时将光栅器块视为碰巧执行固定的函数操作的一组重要的管道阶段之间的接口。 许多这些固定的函数操作可以通过软件开发人员进行调整。

光栅器始终确定输入的位置在剪贴空间内提供、 执行剪切和角度来看除，然后应用视区缩放和偏移量。

Direct3D 运行时调用以下的驱动程序函数，来创建、 设置，并销毁光栅化程序的状态：

[**CalcPrivateRasterizerStateSize**](https://msdn.microsoft.com/library/windows/hardware/ff538298)

[**CreateRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff540676)

[**DestroyRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff552788)

[**SetRasterizerState**](https://msdn.microsoft.com/library/windows/hardware/ff569550)

[**SetScissorRects**](https://msdn.microsoft.com/library/windows/hardware/ff569659)

[**SetViewports**](https://msdn.microsoft.com/library/windows/hardware/ff569698)

 

 





