---
title: 窗口模式行为
description: 窗口模式行为
ms.assetid: a852b1d7-5722-4092-a5ff-338dbb2f77b3
keywords:
- 窗口模式下旋转 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d1a979fabb0abc9edf73ce7021ab11399a2ff8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565587"
---
# <a name="windowed-mode-behavior"></a>窗口模式行为


窗口模式设备的 Microsoft Direct3D 运行时永远不会调用函数的用户模式显示驱动程序，锁定一个旋转主表面上，要呈现到旋转的主图面，或者执行位块传输 (bitblt) 到或从旋转主。 它是窗口模式设备的 Direct3D 运行时处理所有这些情况。

窗口模式设备的 Direct3D 运行时可能不会调用用户模式显示驱动程序[ **OpenResource** ](https://msdn.microsoft.com/library/windows/hardware/ff568611)函数，以打开共享主图面，然后以通知的用户模式显示驱动程序主要的曲面的方向。 但是，如果未运行桌面窗口管理器 (DWM)，Direct3D 运行时将调用*OpenResource*，并且用户模式显示驱动程序有关的主要方向将得到通知。 仅当该驱动程序必须为其自身的用途; 访问 （通过 bitblt 或锁） 的主面必须知道主表面方向的用户模式显示驱动程序窗口模式设备的 Direct3D 运行时永远不会将请求用户模式显示驱动程序来访问旋转主图面。 因此，如果用户模式显示驱动程序必须访问主图面，用于内部用途，驱动程序需要一种机制，除了调用其**OpenResource**函数，因为*OpenResource*不会始终调用。

DWM 或显示微型端口驱动程序[ **DxgkDdiPresent** ](https://msdn.microsoft.com/library/windows/hardware/ff559743)函数将旋转窗口模式数据。

 

 





