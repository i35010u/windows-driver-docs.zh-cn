---
title: 用于反交错的反交错容器设备
description: 用于反交错的反交错容器设备
keywords:
- 取消隔行扫描容器设备 WDK DirectX VA
- 容器设备 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c243cbbbd98fed74c60ff7aac230cd0cc5ea4f18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809597"
---
# <a name="deinterlace-container-device-for-deinterlacing"></a>用于反交错的反交错容器设备


## <span id="ddk_deinterlace_container_device_for_deinterlacing_gg"></span><span id="DDK_DEINTERLACE_CONTAINER_DEVICE_FOR_DEINTERLACING_GG"></span>


只能在 DirectX VA 设备的上下文中使用 [取消隔行扫描的示例函数](sample-functions-for-deinterlacing.md) ，因此必须首先定义和创建隔行扫描容器设备。

如果驱动程序支持对压缩视频进行加速解码，则在由 VMR 启动时，驱动程序还会创建两个更多的 DirectX VA 设备：一个用于执行视频解码工作，另一个用于执行取消隔行扫描操作。

**注意**   取消隔行扫描容器设备只是一种软件构造，不代表设备上包含的任何功能硬件。

 

 

 





