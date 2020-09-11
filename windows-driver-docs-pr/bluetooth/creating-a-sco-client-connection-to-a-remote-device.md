---
title: 创建到远程设备的 SCO 客户端连接
description: 创建到远程设备的 SCO 客户端连接
ms.assetid: e5a4ed14-1fb0-4a5f-b388-5e536d674c23
keywords:
- 面向同步连接的 WDK 蓝牙
- SCO profile 驱动程序 WDK 蓝牙
- 启动 SCO 连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d22524a2195ee007426a638c261005655e82903
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010421"
---
# <a name="creating-a-sco-client-connection-to-a-remote-device"></a>创建到远程设备的 SCO 客户端连接


SCO 客户端配置文件驱动程序是一个配置文件驱动程序，它向远程设备请求) 连接的面向同步连接 (SCO。 如果设备接受连接，则会通知 SCO 客户端配置文件驱动程序对连接所做的任何更改。 例如，SCO 客户端配置文件驱动程序可以请求连接到远程耳机，然后在耳机接受连接请求后，当耳机关闭或删除时，蓝牙驱动程序堆栈可以通知配置文件驱动程序。

由于 SCO 连接是两个 Bluetooth 设备之间的点到点连接，因此 SCO 客户端配置文件驱动程序只需要远程设备的蓝牙地址即可连接到。

若要启动到远程设备的 SCO 连接，配置文件驱动程序应 [生成并发送](building-and-sending-a-brb.md) [**BRB \_ SCO \_ 开放式 \_ 通道**](/previous-versions/ff536626(v=vs.85)) 请求。

如果远程设备接受配置文件驱动程序的 SCO 连接请求，则配置文件驱动程序可以通过使用 IOCTL INTERNAL BTH SUBMIT BRB 在新连接的通道上执行其他 BRB 命令 \_ \_ \_ \_ ，其中包括：

-   [**BRB \_ SCO \_ 获取 \_ 通道 \_ 信息**](/previous-versions/ff536624(v=vs.85))

-   [**BRB \_ SCO \_ 获取 \_ 系统 \_ 信息**](/previous-versions/ff536625(v=vs.85))

-   [**BRB \_ SCO \_ 传输**](/previous-versions/ff536629(v=vs.85))

**注意**   配置文件驱动程序应在初始化期间[生成并发送](building-and-sending-a-brb.md) **BRB \_ SCO \_ GET \_ 系统 \_ 信息**请求，以确定基础硬件是否支持 SCO，如果是，则全局 SCO 设置是什么。

 

当配置文件驱动程序不再需要与远程设备的 SCO 连接时，它应 [生成并发送](building-and-sending-a-brb.md) [**BRB \_ SCO \_ CLOSE \_ 通道**](/previous-versions/ff536622(v=vs.85)) 请求。

 

