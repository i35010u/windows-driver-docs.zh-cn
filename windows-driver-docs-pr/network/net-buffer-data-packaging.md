---
title: NET_BUFFER 数据打包
description: NET_BUFFER 数据打包
ms.assetid: f0d539ab-c6ed-4cd9-9891-ef4235016d50
keywords:
- NDIS WDK、 发送和接收数据
- 数据打包 WDK 网络
- 发送数据 WDK 网络
- 接收数据 WDK 网络
- NDIS_PACKET
- NET_BUFFER 数据打包 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19adce4ead2584e144d610ab35e1d2b08af66c72
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363319"
---
# <a name="netbuffer-data-packaging"></a>NET\_缓冲区数据打包





在 NDIS 6.0 中重新设计了数据打包。 发送和接收为基础的体系结构[ **NDIS\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff557086)结构已被替换为基础的体系结构[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)并[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 NET\_缓冲区结构是在功能上等同的 NDIS\_数据包结构。 NET\_缓冲区结构 NDIS、 协议驱动程序和微型端口驱动程序指定的网络数据，以及保留的空间的缓冲区 （MDL 链）。 NET\_缓冲区结构可以链接在一起，在列表中描述的 NET\_缓冲区\_列表结构。 NET\_缓冲区\_列表结构还为适用于所有 NET 的带外 (OOB) 数据提供存储\_缓冲区列表中的结构。

Microsoft 下一代网络驱动程序堆栈，包括 TCP/IP 传输和 Winsock 中的所有组件都使用 NET\_缓冲区数据打包。 在整个驱动程序堆栈的统一数据打包无需重新打包数据、 简化数据处理，并减少函数调用数。

以适应旧驱动程序使用 NDIS\_数据包结构，NDIS 6.0 转换 NDIS\_NET 到数据包结构\_缓冲区结构，反之亦然。 这种转换是透明的 NDIS 驱动程序。

NDIS 将传播到更高级别的驱动程序的驱动程序的数据回填要求。 当分配 NET\_缓冲区和 NET\_缓冲区\_列表结构发送数据，更高级别的驱动程序分配足够的数据空间来容纳较低级别堆栈中的所有驱动程序。 因此，较低级别的驱动程序不需要分配更多的缓冲区空间来容纳特定于层的标头。 相反，它们可以实现此目的使用回填预分配的空间。

详细了解 NET\_缓冲区体系结构，请参阅[NET\_缓冲体系结构](net-buffer-architecture.md)。

 

 





