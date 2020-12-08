---
title: 用户模式显示驱动程序的线程模型
description: 用户模式显示驱动程序的线程模型
keywords:
- 线程 WDK 显示，用户模式驱动程序
- 同步 WDK 显示，用户模式驱动程序
- 用户模式显示驱动程序 WDK Windows Vista，同步
- 用户模式显示驱动程序 WDK Windows Vista，线程处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c627b7e36eef3d0a0f6f95e0abde41108ad6eaa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820789"
---
# <a name="threading-model-of-user-mode-display-driver"></a>用户模式显示驱动程序的线程模型


## <span id="ddk_thread_model_of_user_mode_display_driver_gg"></span><span id="DDK_THREAD_MODEL_OF_USER_MODE_DISPLAY_DRIVER_GG"></span>


用户模式显示驱动程序不会同时加载到多个进程中--用户模式显示驱动程序 DLL 单独加载到每个进程的地址空间中。 尽管如此，多个线程也可以同时在用户模式显示驱动程序中运行。 但是，在用户模式显示驱动程序中运行的每个线程都必须访问不同的显示设备，该显示设备是通过调用用户模式显示驱动程序的 [**CreateDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice) 函数创建的。 例如：

-   创建两个 Microsoft Direct3D 设备的应用程序可以有两个线程，分别访问这些设备。

-   应用程序可以在两个不同的线程上使用一台 Direct3D 设备，该9.0 设备与 DirectX 5.0 运行时创建的 Microsoft DirectDraw 设备一起创建。

**注意**   使用同一个显示设备的两个或多个线程永远不能同时在用户模式显示驱动程序中运行。

 

与显示微型端口驱动程序一样，用户模式显示驱动程序不需要使用任何全局数据结构，因为 Direct3D 设备是独立的，并且每个设备的状态和资源不会影响其他设备。 如果用户模式显示驱动程序必须维护全局跨设备数据结构 (例如，对于自定义系统内存堆管理器) ，它必须通过使用其自己的机制来对访问进行仲裁。 强烈建议不要驱动程序管理的此类全局数据结构。 因为 Direct3D 运行时在必须访问资源的每个用户模式显示设备中都打开一个独立的共享资源的 "视图"，所以，不应与单个进程或设备使用的资源不同地处理跨进程或跨设备资源。 生存期和其他管理由 DirectX 图形内核子系统 (*Dxgkrnl.sys*) 处理。

在多处理器计算机上，Direct3D 运行时可能会从工作线程调用用户模式显示驱动程序，而不是从主应用程序线程调用。 这种多处理器优化对于用户模式显示驱动程序是透明的。 当运行时使用多处理器优化时，它仍可确保在任何给定时间，只有一个引用特定设备的线程在驱动程序中运行。

 

