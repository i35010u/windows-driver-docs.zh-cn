---
title: 完全类型化后端缓冲区强制转换
description: 完全类型化后端缓冲区强制转换
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，强制转换完全类型的后台缓冲区
- 强制转换完全类型的后台缓冲区 WDK Windows 7 显示
- 后台缓冲区 WDK Windows 7 显示
- 后台缓冲区 WDK Windows 7 显示，完全键入
- 完全类型的后台缓冲区 WDK Windows 7 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d4c8fe871e457065be5c758eb3590a9131ca808
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828097"
---
# <a name="fully-typed-back-buffers-casting"></a>完全类型化后端缓冲区强制转换


本部分仅适用于 Windows 7 及更高版本的操作系统。

考虑通过调用驱动程序的 [**CreateResource (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)函数创建的资源，并将 [**D3D10DDIARG \_ CreateResource**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)结构的 **format** 成员设置为系列 DXGI \_ 格式 R8G8B8A8 无类型 \_ \_ 、dxgi 格式 B8G8R8A8 无类型或 dxgi 格式 R10G10B10A2 无类型，并在 D3D10 \_ \_ \_ \_ \_ \_ \_ \_ \_ **\_ BindFlags** 的 **D3D10DDIARG** 成员中设置 CreateResource DDI BIND。 Direct3D 版本10.1 运行时随后可以使用适当系列 (的任何完全类型的成员（例如，B8G8R8A8 UNORM SRGB for DXGI format B8G8R8A8 无类型族) ）来创建视图 (呈现目标或着色器资源) ， \_ \_ \_ \_ \_ \_ \_ 即使原始资源创建为完全类型。 如果 \_ 没有为 \_ 资源设置 D3D10 DDI 绑定 \_ ，则不允许进行此重转换，这与 Direct3D 版本10中所有完全类型的资源的情况相同。

Direct3D 版本10.1 的这一更改允许应用程序以 \_ \_ \_ dxgi 格式 R8G8B8A8 UNORM SRGB 重新查看 dxgi 格式 R8G8B8A8 UNORM 后台缓冲区 \_ \_ \_ \_ ，反之亦然。 此更改还允许应用程序为 DXGI 格式 \_ B8G8R8A8 UNORM 强制转换 dxgi 格式 \_ B8G8R8A8 \_ UNORM \_ SRGB 后台缓冲区 \_ \_ \_ ，并重新查看 dxgi 格式 \_ \_ R10G10B10 \_ \_ \_ \_ \_ \_ \_ \* XR

 

