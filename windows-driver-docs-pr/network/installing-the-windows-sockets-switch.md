---
title: 安装 Windows Sockets 交换机
description: 安装 Windows Sockets 交换机
keywords:
- Windows Socket Direct WDK，安装组件
- 分层服务提供商 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8faf00800772d89fcfdc640eb6acb68f43b2d6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815977"
---
# <a name="installing-the-windows-sockets-switch"></a>安装 Windows Sockets 交换机





Microsoft Windows 将 Windows 套接字交换机作为 *分层服务提供程序* 安装，Windows 套接字服务提供程序接口 (SPI) 同时作为顶部和底部接口。 与 TCP/IP 服务提供程序一样，交换机会导出 TCP/IP 的协议特征。 开关是第一个可见的 TCP/IP 提供程序，这使得此开关成为为 [WSK 地址系列](ws2def-h.md)打开套接字的应用程序的默认选项。

 

