---
title: 窗口模式行为
description: 窗口模式行为
ms.assetid: a852b1d7-5722-4092-a5ff-338dbb2f77b3
keywords:
- 窗口模式旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018d8f85bbf6eb091232c5aa7f04be0c3b3cbb27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829144"
---
# <a name="windowed-mode-behavior"></a>窗口模式行为


对于窗口模式设备，Microsoft Direct3D 运行时永远不会调用用户模式显示驱动程序的功能来锁定旋转后的主表面、呈现到旋转的主表面，或执行到旋转后的主表面的位块传输（bitblt）。 也就是说，窗口模式设备的 Direct3D 运行时将处理所有这些情况。

窗口模式设备的 Direct3D 运行时可能不会调用用户模式显示驱动程序的[**OpenResource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)函数来打开共享主表面，并通知用户模式显示驱动程序的主表面。 但是，如果桌面窗口管理器（DWM）未运行，Direct3D 运行时将调用*OpenResource*，并通知用户模式显示驱动程序的主要方向。 仅当驱动程序必须访问主表面（通过 bitblt 或锁定）才能自行使用时，用户模式显示驱动程序才必须知道主表面方向;用于窗口模式设备的 Direct3D 运行时将不会请求用户模式显示驱动程序访问旋转的主表面。 因此，如果用户模式显示驱动程序必须访问主表面来实现其自己的内部用途，则驱动程序除了需要调用其**OpenResource**函数外，还需要一种机制，因为*OpenResource*不会始终调用。

DWM 或显示微型端口驱动程序的[**DxgkDdiPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)函数会旋转窗口模式数据。

 

 





