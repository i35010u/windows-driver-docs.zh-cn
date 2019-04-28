---
title: 多重采样渲染
description: 多重采样渲染
ms.assetid: 7c21b0e0-bdd3-4de3-a5c5-5adc2d2e2b33
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多重采样呈现
- multisample 呈现 WDK DirectX 8.0
- 呈现 multisamples WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac2985f20054db932b8ab2bfe9d32dec00117cdb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345557"
---
# <a name="multisample-rendering"></a>多重采样渲染


## <span id="ddk_multisample_rendering_gg"></span><span id="DDK_MULTISAMPLE_RENDERING_GG"></span>


DirectX 8.0 引入了针对使用的每个应用程序控制下的像素的样本数的多重采样呈现支持。 **IDirect3DDevice8**接口在全屏幕和开窗操作模式中支持多重采样。 此外，没有足够的灵活性以支持执行到像素在后端 （直接从帧缓冲区中） 或 （通过特殊的翻转或 blt 调用） 的前端的示例处理的硬件。有关详细信息**IDirect3DDevice8**，请参阅 DirectX 8.0 文档。

 

 





