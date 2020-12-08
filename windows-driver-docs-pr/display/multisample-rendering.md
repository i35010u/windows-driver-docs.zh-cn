---
title: 多重采样渲染
description: 多重采样渲染
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多级显示
- 以多级显示方式呈现 WDK DirectX 8。0
- 呈现 multisamples WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4304da627c1eeff4f2f6d2ddbd43ec5ef1f42e57
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840381"
---
# <a name="multisample-rendering"></a>多重采样渲染


## <span id="ddk_multisample_rendering_gg"></span><span id="DDK_MULTISAMPLE_RENDERING_GG"></span>


DirectX 8.0 引入了针对应用程序控制下每个像素的样本数的多级显示支持。 **IDirect3DDevice8** 接口支持全屏和窗口操作模式下的多级。 此外，还可以灵活地支持硬件，使其能够在后端 (直接移出帧缓冲区) 或前端 (通过特殊的翻转或 blt 调用) 来处理示例。有关 **IDirect3DDevice8** 的详细信息，请参阅 DirectX 8.0 文档。

 

 





