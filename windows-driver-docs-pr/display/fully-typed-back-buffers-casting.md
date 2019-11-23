---
title: 完全类型化后端缓冲区强制转换
description: 完全类型化后端缓冲区强制转换
ms.assetid: d34f95a4-e380-4bfb-9909-0938f63174be
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，强制转换完全类型的后台缓冲区
- 强制转换完全类型的后台缓冲区 WDK Windows 7 显示
- 后台缓冲区 WDK Windows 7 显示
- 后台缓冲区 WDK Windows 7 显示，完全键入
- 完全类型的后台缓冲区 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef211bc2376b7952b8c36d61c600731f06d9d9fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839688"
---
# <a name="fully-typed-back-buffers-casting"></a>完全类型化后端缓冲区强制转换


本部分仅适用于 Windows 7 及更高版本的操作系统。

请考虑通过对驱动程序的[**CreateResource （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)函数的调用创建的资源，将[**D3D10DDIARG\_CreateResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)结构的**FORMAT**成员设置为系列 DXGI\_格式\_R8G8B8A8\_无类型，dxgi\_格式\_B8G8R8A8\_无类型或 dxgi\_格式\_R10G10B10A2\_无类型和 D3D10\_ **D3D10DDIARG\_CREATERESOURCE**的 BindFlags 成员。\_\_ Direct3D 版本10.1 运行时可以通过使用适当系列的任何完全类型的成员（例如，DXGI\_FORMAT\_B8G8R8A8\_UNORM\_SRGB 用于 DXGI\_格式，在这些资源上创建视图（呈现目标或着色器资源），即使将原始资源创建为完全类型。\_\_ 如果没有为资源设置 D3D10\_DDI\_绑定\_，则不允许进行此重转换，这与 Direct3D 版本10中所有完全类型的资源的情况相同。

Direct3D 版本10.1 的这一更改允许应用程序以\_R8G8B8A8\_UNORM 后台缓冲区的\_\_方式重新查看 DXGI\_格式。\_\_ 此更改还允许应用程序将 DXGI\_格式转换\_B8G8R8A8\_UNORM\_SRGB 后台缓冲区，以实现 DXGI\_格式\_B8G8R8A8\_UNORM，并重新查看 DXGI\_格式\_R10G10B10\_XR\_\_\_\_\_\_\*

 

 





