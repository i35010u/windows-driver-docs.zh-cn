---
title: 用户模式显示驱动程序的线程模型
description: 用户模式显示驱动程序的线程模型
ms.assetid: 43bb6032-5f34-434b-8404-aef6a424a2ee
keywords:
- 线程处理 WDK 显示，用户模式驱动程序
- 同步 WDK 显示，用户模式驱动程序
- 用户模式显示驱动程序 WDK Windows Vista 中，同步
- 用户模式显示驱动程序 WDK Windows Vista 中，线程处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8b00faec1048361c6d2fd305ffa94dc6628dfdd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354677"
---
# <a name="threading-model-of-user-mode-display-driver"></a>用户模式显示驱动程序的线程模型


## <span id="ddk_thread_model_of_user_mode_display_driver_gg"></span><span id="DDK_THREAD_MODEL_OF_USER_MODE_DISPLAY_DRIVER_GG"></span>


用户模式显示驱动程序未加载到多个进程同时-用户模式显示驱动程序 DLL 单独加载到每个进程的地址空间。 尽管如此，多个线程可以运行在用户模式显示驱动程序在同一时间。 但是，在用户模式显示驱动程序中运行每个线程必须访问不同的显示设备，创建的用户模式显示驱动程序的调用[ **CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice)函数。 例如：

-   创建两个 Microsoft Direct3D 设备的应用程序可以独立地访问这些设备的两个线程。

-   应用程序可以使用，对两个不同的线程，以及 DirectX 5.0 运行时创建的 Microsoft DirectDraw 设备的 Microsoft DirectX 9.0 Direct3D 运行时创建的 Direct3D 设备。

**请注意**  使用相同的显示设备的两个或多个线程可以永远不会在用户模式显示驱动程序中同时运行。

 

显示微型端口驱动程序，如用户模式显示驱动程序不需要使用的任何全局数据结构，因为 Direct3D 设备无关，并且状态和从每个设备的资源不影响其他设备。 如果用户模式显示驱动程序必须维护跨设备的全局数据结构 (例如，对于自定义系统内存堆管理器)，它必须进行访问仲裁使用自己的机制。 该驱动程序管理的结构强烈建议不要使用此类全局数据。 Direct3D 运行时将在每个用户模式下显示设备都必须访问的资源中打开独立的共享资源"视图"，因为跨进程或跨设备的资源不应处理以不同的方式从单个处理的资源或设备使用。 生存期和其他管理步骤将由 DirectX 图形内核子系统 (*Dxgkrnl.sys*)。

在多处理器计算机上 Direct3D 运行时可能会从工作线程，而不是从主应用程序线程调用的用户模式显示驱动程序。 此多处理器优化是透明的用户模式显示驱动程序。 当运行时使用多个处理器优化时，它仍会确保引用特定的设备只有一个线程运行在驱动程序在任何给定时间。

 

 





