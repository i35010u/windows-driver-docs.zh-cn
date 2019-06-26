---
title: BGRA 扫描输出支持
description: BGRA 扫描输出支持
ms.assetid: 88ef5de7-59cc-4a8a-aaf7-74489a7ac0ab
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，BGRA 扫描扩展支持
- BGRA 扫描扩展支持 WDK Windows 7 显示
- 扫描扩展支持 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17e2bb0b87036ca5023220559f7c23bc6f43cfb9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384628"
---
# <a name="bgra-scan-out-support"></a>BGRA 扫描输出支持


本部分仅适用于 Windows 7 和更高版本的操作系统。

扫描出位开启 DXGI\_格式\_B8G8R8A8\_UNORM 和 DXGI\_格式\_B8G8R8A8\_UNORM\_SRGB 格式。 因此，用户模式显示驱动程序应该能够执行以下操作：

-   这些格式中的处理请求的主图面。

-   处理对调用其[ **SetDisplayMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymode)函数使用这些格式创建的资源。

-   处理对调用其[ **PresentDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数来提供这两种位块传输 (bitblt) 通过这些格式和翻转操作。

-   处理对调用其[ **BltDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数以复制通过 stretch，旋转，这些格式，并解决 （事实上是预期的 RGBA 变体的所有 bitblt 操作）。

 

 





