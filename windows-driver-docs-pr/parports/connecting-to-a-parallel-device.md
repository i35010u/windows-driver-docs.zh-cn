---
title: 连接到并行设备
description: 连接到并行设备
ms.assetid: c05a1a1e-308a-4b9f-af43-761c4c14d6af
keywords:
- 并行 WDK，连接的设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec8aa8e7076f59f93b6168b6204ec5e2b439f4d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373552"
---
# <a name="connecting-to-a-parallel-device"></a>连接到并行设备





客户端用[ **IOCTL\_内部\_PARCLASS\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/ff544040)请求以获取[ **PARCLASS\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff544334)结构，其中包含：

-   分配给并行端口 I/O 资源

-   硬件功能的并行端口

-   请参阅内核模式驱动程序可用于设置并行的设备-IEEE 1284 运行模式的回调例程的指针[设置和清除并行设备的通信模式](setting-and-clearing-a-communication-mode-for-a-parallel-device.md)

-   指向回调例程的内核模式驱动程序可用于读取和写入并行设备-请参阅[读取和写入并行设备](reading-and-writing-a-parallel-device.md)。

回调例程提供典型功能驱动程序需要的功能。 使用回调例程是比使用等效的设备控制请求更加有效。

从设备使用的客户端断开[ **IOCTL\_内部\_PARCLASS\_断开连接**](https://msdn.microsoft.com/library/windows/hardware/ff544046)请求。

 

 




