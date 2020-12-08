---
title: 管理多个 GPU 方案的资源
description: 管理多个 GPU 方案的资源
keywords:
- GPU WDK Windows 7 显示
- GPU WDK Windows 7 显示，多个
- GPU WDK Windows 7 显示，多个，管理资源
- 多个 Gpu，WDK Windows 7 显示
- 多 Gpu WDK Windows 7 显示，管理资源
- GPU WDK Windows 2008 资源 R2 显示
- GPU WDK Windows 2008 资源 R2 显示，多个
- GPU WDK Windows 2008 资源 R2 显示、多个，管理资源
- 多个 Gpu，WDK Windows 2008 资源 R2 显示
- 多 Gpu WDK Windows 2008 资源 R2 显示，管理资源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6215e8643bd640b48fbaf20d58d6e6e1b7547445
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793887"
---
# <a name="managing-resources-for-multiple-gpu-scenarios"></a>管理多个 GPU 方案的资源


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

为了适当地管理多个 GPU 方案的资源，用户模式显示驱动程序可以实现 Windows 7 附带 (DDI) 的新设备驱动程序接口。 每个资源可能会分割到内存中，以便在多个 Gpu 上进行呈现。 驱动程序可以实现这一新的 DDI 来重新合并每个资源，以使新资源所有者具有合并资源。 在此 DDI 实现中，驱动程序必须刷新可能会修改资源的任何部分生成的命令缓冲区。 此 DDI 作为对 [direct3d 版本 9 ddi](/windows-hardware/drivers/ddi/d3dumddi/index) 和 [DIRECT3D 版本 10 DXGI ddi](/windows-hardware/drivers/ddi/index)的扩展提供。 驱动程序可以实现 [**ResolveSharedResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_resolvesharedresource) 来支持 Microsoft direct3d 功能级别9和 [**ResolveSharedResourceDXGI**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_1_ddi_base_functions) ，以支持 Direct3D 功能级别10和11。

从 Windows 8.1 开始，用户模式驱动程序可以支持在离散 GPU 和集成 GPU 之间共享的跨适配器资源。 请参阅 [在混合系统中使用跨适配器资源](using-cross-adapter-resources-in-a-hybrid-system.md)。

 

