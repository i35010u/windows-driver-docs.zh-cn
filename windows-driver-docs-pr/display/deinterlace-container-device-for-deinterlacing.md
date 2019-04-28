---
title: 用于反交错的反交错容器设备
description: 用于反交错的反交错容器设备
ms.assetid: e14db243-46e5-4ab3-b134-8aadfa99e614
keywords:
- 取消隔行扫描容器设备 WDK DirectX VA
- 容器设备 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 157b49a4e111a86084baff0668ed45c1b079e2b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348917"
---
# <a name="deinterlace-container-device-for-deinterlacing"></a>用于反交错的反交错容器设备


## <span id="ddk_deinterlace_container_device_for_deinterlacing_gg"></span><span id="DDK_DEINTERLACE_CONTAINER_DEVICE_FOR_DEINTERLACING_GG"></span>


[示例的去隔行函数](sample-functions-for-deinterlacing.md)因此需要先定义并创建取消隔行扫描容器设备只可以 DirectX VA 设备上下文中使用。

如果驱动程序支持加速的解码压缩的视频，由 VMR 启动时，该驱动程序还会创建两个更多的 DirectX VA 设备： 一个用来执行解码工作，另一个用于执行取消隔行扫描操作的视频。

**请注意**  取消隔行扫描容器设备是软件构造并不表示任何包含的设备上起作用的硬件。

 

 

 





