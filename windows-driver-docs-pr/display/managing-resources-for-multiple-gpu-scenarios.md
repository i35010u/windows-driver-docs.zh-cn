---
title: 管理多个 GPU 方案的资源
description: 管理多个 GPU 方案的资源
ms.assetid: f3dc10b1-76e9-4f31-b253-149b6300611d
keywords:
- GPU WDK Windows 7 显示
- GPU WDK Windows 7 显示，多个
- GPU WDK Windows 7 显示，多个，管理资源
- 多个 Gpu WDK Windows 7 显示
- 多个 Gpu WDK Windows 7 显示、 管理资源
- GPU WDK Windows 2008 资源 R2 显示
- GPU WDK Windows 2008 资源 R2 显示，多个
- GPU WDK Windows 2008 资源 R2 显示，多个，管理资源
- 多个 Gpu WDK Windows 2008 资源 R2 显示
- 多个 Gpu WDK Windows 2008 资源 R2 显示、 管理资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7185420264d2114b6b4a3a94054d076adfa4c03d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379862"
---
# <a name="managing-resources-for-multiple-gpu-scenarios"></a>管理多个 GPU 方案的资源


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

若要适当地管理多个 GPU 方案的资源，用户模式显示驱动程序可以实现新设备驱动程序接口 (DDI) 随 Windows 7。 每个资源可能会分散的多个 Gpu 上呈现的内存。 该驱动程序可以实现此新 DDI 重新合并的每个资源，以便新的资源所有者已合并的资源。 在此 DDI 实现中，该驱动程序必须刷新可能会修改资源任何部分生成的命令缓冲区。 为扩展提供此 DDI [Direct3D 版本 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/index)进出[Direct3D 版本 10 DXGI DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 该驱动程序可以实现[ **ResolveSharedResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_resolvesharedresource)以支持 Microsoft Direct3D 功能级别 9 并[ **ResolveSharedResourceDXGI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_1_ddi_base_functions)来支持 Direct3D 功能级别 10 和 11。

从 Windows 8.1，用户模式驱动程序可以支持跨适配器是分立的 GPU 和集成的 GPU 之间共享的资源。 请参阅[混合系统中使用跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)。

 

 





