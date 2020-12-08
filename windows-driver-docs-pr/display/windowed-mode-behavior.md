---
title: 窗口模式行为
description: 窗口模式行为
keywords:
- 窗口模式旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ca85e2ea666c6967d53143099c8b7b490945590
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826027"
---
# <a name="windowed-mode-behavior"></a>窗口模式行为


对于窗口模式设备，Microsoft Direct3D 运行时永远不会调用用户模式显示驱动程序的功能来锁定旋转后的主表面、呈现到旋转的主表面，或执行从旋转的主表面 (bitblt) 的位块传输。 也就是说，窗口模式设备的 Direct3D 运行时将处理所有这些情况。

窗口模式设备的 Direct3D 运行时可能不会调用用户模式显示驱动程序的 [**OpenResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource) 函数来打开共享主表面，并通知用户模式显示驱动程序的主表面。 但是，如果桌面窗口管理器 (DWM) 未运行，Direct3D 运行时将调用 *OpenResource*，并通知用户模式显示驱动程序的主要方向。 仅当驱动程序必须通过 bitblt 或锁定) 访问主 (表面时，用户模式显示驱动程序才必须知道主表面方向;用于窗口模式设备的 Direct3D 运行时将不会请求用户模式显示驱动程序访问旋转的主表面。 因此，如果用户模式显示驱动程序必须访问主表面来实现其自己的内部用途，则驱动程序除了需要调用其 **OpenResource** 函数外，还需要一种机制，因为 *OpenResource* 不会始终调用。

DWM 或显示微型端口驱动程序的 [**DxgkDdiPresent**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present) 函数会旋转窗口模式数据。

 

