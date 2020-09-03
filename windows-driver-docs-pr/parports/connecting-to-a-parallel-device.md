---
title: 连接到并行设备
description: 连接到并行设备
ms.assetid: c05a1a1e-308a-4b9f-af43-761c4c14d6af
keywords:
- 并行设备 WDK，连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a1e3a403a209381d095088180d164cb9cf9f3ea
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89385003"
---
# <a name="connecting-to-a-parallel-device"></a>连接到并行设备





客户端使用 [**IOCTL \_ INTERNAL \_ PARCLASS \_ CONNECT**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_connect) 请求获取包含以下内容的 [**PARCLASS \_ 信息**](/windows-hardware/drivers/ddi/parallel/ns-parallel-_parclass_information) 结构：

-   分配给并行端口的 i/o 资源

-   并行端口的硬件功能

-   指向回调例程的指针，内核模式驱动程序可以使用这些例程为并行设备设置 IEEE 1284 操作模式-请参阅 [设置和清除并行设备的通信模式](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

-   指向内核模式驱动程序可用于读取和写入并行设备的回调例程的指针，请参阅 [读取和写入并行设备](reading-and-writing-a-parallel-device.md)。

回调例程提供典型功能驱动程序需要的功能。 使用回调例程比使用等效的设备控制请求更为有效。

客户端通过使用 [**IOCTL \_ 内部 \_ PARCLASS \_ 断开连接**](/windows-hardware/drivers/ddi/parallel/ni-parallel-ioctl_internal_parclass_disconnect) 请求断开与设备的连接。

 

