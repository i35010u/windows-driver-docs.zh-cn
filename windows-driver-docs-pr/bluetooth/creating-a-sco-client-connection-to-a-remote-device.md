---
title: 创建 SCO 客户端连接到远程设备
description: 创建 SCO 客户端连接到远程设备
ms.assetid: e5a4ed14-1fb0-4a5f-b388-5e536d674c23
keywords:
- 同步面向连接的 WDK 蓝牙
- SCO 配置文件驱动程序 WDK 蓝牙
- 启动 SCO 连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19bcc017d23799c5c4af684d476dad10b91c4984
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520553"
---
# <a name="creating-a-sco-client-connection-to-a-remote-device"></a>创建 SCO 客户端连接到远程设备


SCO 客户端配置文件驱动程序是请求 Synchronous Connection-Oriented (SCO) 连接到远程设备的配置文件驱动程序。 如果设备接受连接，连接到任何更改通知 SCO 客户端配置文件驱动程序。 例如，SCO 客户端配置文件驱动程序可以请求连接到远程耳机，并将耳机接受连接请求后，蓝牙驱动程序堆栈耳机处于关闭状态时，可以通知配置文件驱动程序或删除。

SCO 连接都是两个蓝牙设备之间的点对点连接，因为 SCO 客户端配置文件驱动程序需要连接到远程设备的蓝牙地址。

若要启动的 SCO 连接到远程设备，配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_SCO\_打开\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536626)请求。

如果远程设备接受配置文件驱动程序的 SCO 连接请求，该配置文件驱动程序然后使用可以执行其他 BRB 命令跨整个新连接的通道 IOCTL\_内部\_同时为\_提交\_BRB，包括：

-   [**BRB\_SCO\_GET\_CHANNEL\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536624)

-   [**BRB\_SCO\_GET\_SYSTEM\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff536625)

-   [**BRB\_SCO\_TRANSFER**](https://msdn.microsoft.com/library/windows/hardware/ff536629)

**请注意**  配置文件驱动程序应[生成并发送](building-and-sending-a-brb.md) **BRB\_SCO\_获取\_系统\_信息**期间请求若要确定是否基础硬件支持 SCO，那么，哪些全局 SCO 设置是如果的初始化。

 

当配置文件驱动程序不再需要 SCO 连接到远程设备时，它应[生成并发送](building-and-sending-a-brb.md) [ **BRB\_SCO\_关闭\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff536622)请求。

 

 





