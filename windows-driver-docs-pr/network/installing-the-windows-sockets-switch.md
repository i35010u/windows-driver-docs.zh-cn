---
title: 安装 Windows Sockets 交换机
description: 安装 Windows Sockets 交换机
ms.assetid: 69cdec9f-8ed7-48d7-ae6d-a9a9916e3c58
keywords:
- Windows Socket Direct WDK，安装组件
- 分层服务提供商 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e02918587353bfe46ea7e41c55bc82f468331ab
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207289"
---
# <a name="installing-the-windows-sockets-switch"></a>安装 Windows Sockets 交换机





Microsoft Windows 将 Windows 套接字交换机作为 *分层服务提供程序*安装，Windows 套接字服务提供程序接口 (SPI) 同时作为顶部和底部接口。 与 TCP/IP 服务提供程序一样，交换机会导出 TCP/IP 的协议特征。 开关是第一个可见的 TCP/IP 提供程序，这使得此开关成为为 [WSK 地址系列](/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))打开套接字的应用程序的默认选项。

 

