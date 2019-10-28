---
title: BGRA 扫描输出支持
description: BGRA 扫描输出支持
ms.assetid: 88ef5de7-59cc-4a8a-aaf7-74489a7ac0ab
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，BGRA 扫描支持
- BGRA 扫描支持 WDK Windows 7 显示
- 扫描支持 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f96d95af52ab090d3625a65822b3d7967cb819c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839070"
---
# <a name="bgra-scan-out-support"></a>BGRA 扫描输出支持


本部分仅适用于 Windows 7 及更高版本的操作系统。

为 DXGI\_格式启用了扫描位\_B8G8R8A8\_UNORM 和 DXGI\_格式\_B8G8R8A8\_UNORM\_SRGB 格式。 因此，用户模式显示驱动程序应该能够执行以下操作：

-   处理采用这些格式的主表面的请求。

-   对于用这些格式创建的资源，处理其[**SetDisplayMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setdisplaymode)函数的调用。

-   通过两个位块传输（bitblt）和翻转操作处理对其[**PresentDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数的调用以呈现这些格式。

-   处理对其[**BltDXGI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)函数的调用，以通过拉伸、旋转和解析（事实上，需要为 RGBA 变体的所有 bitblt 操作）复制这些格式。

 

 





