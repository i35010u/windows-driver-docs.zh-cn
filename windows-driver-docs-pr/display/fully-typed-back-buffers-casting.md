---
title: 完全类型化后端缓冲区强制转换
description: 完全类型化后端缓冲区强制转换
ms.assetid: d34f95a4-e380-4bfb-9909-0938f63174be
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，并完全类型化后台缓冲区进行类型转换
- 返回转换完全类型化缓冲 WDK Windows 7 显示
- 后缓冲 WDK Windows 7 显示
- 返回缓冲区 WDK Windows 7 显示，完全类型化
- 显示完全类型化后台缓冲区 WDK Windows 7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58b8e7cbc740fdd039ec68e8c4c22b2a0f1ccc31
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372967"
---
# <a name="fully-typed-back-buffers-casting"></a>完全类型化后端缓冲区强制转换


本部分仅适用于 Windows 7 和更高版本的操作系统。

请考虑通过驱动程序的调用创建的资源[ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)函数与**格式**隶属[ **D3D10DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)结构设置为的格式为系列 DXGI\_格式\_R8G8B8A8\_TYPELESS、 DXGI\_格式\_B8G8R8A8\_TYPELESS 或 DXGI\_格式\_R10G10B10A2\_TYPELESS 和 D3D10\_DDI\_绑定\_中设置的现值**BindFlags**的成员**D3D10DDIARG\_CREATERESOURCE**。 Direct3D 版本 10.1 运行时可以随后创建的视图 （呈现目标或着色器资源） 在这些资源上使用任何相应系列的完全类型化成员 (例如，DXGI\_格式\_B8G8R8A8\_UNORM\_dxgi SRGB\_格式\_B8G8R8A8\_无类型系列)，即使原始资源创建为已完全类型化。 如果 D3D10\_DDI\_绑定\_资源未设置存在，则重新转换不允许，Direct3D 版本 10 中的所有完全类型化资源的情况一样。

Direct3D 版本 10.1 此更改允许应用程序重新查看 DXGI\_格式\_R8G8B8A8\_UNORM 后台缓冲区作为 DXGI\_格式\_R8G8B8A8\_UNORM\_SRGB，反之亦然。 此更改还使应用程序转换 DXGI\_格式\_B8G8R8A8\_UNORM\_SRGB 后台缓冲区的 DXGI\_格式\_B8G8R8A8\_UNORM 并重新查看 DXGI\_格式\_R10G10B10\_XR\_偏差\_A2\_作为 DXGI UNORM\_格式\_R10G10B10A2\_ \*为呈现。

 

 





