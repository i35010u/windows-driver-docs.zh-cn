---
title: 安装 Windows Sockets 交换机
description: 安装 Windows Sockets 交换机
ms.assetid: 69cdec9f-8ed7-48d7-ae6d-a9a9916e3c58
keywords:
- Windows Socket Direct WDK，安装组件
- 分层服务提供商 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e73bfdd0701e0ed4b894e4220212ef87447b247
ms.sourcegitcommit: 409dd20db50c58b817ef985048fb7aab952cb0ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93244856"
---
# <a name="installing-the-windows-sockets-switch"></a>安装 Windows Sockets 交换机





Microsoft Windows 将 Windows 套接字交换机作为 *分层服务提供程序* 安装，Windows 套接字服务提供程序接口 (SPI) 同时作为顶部和底部接口。 与 TCP/IP 服务提供程序一样，交换机会导出 TCP/IP 的协议特征。 开关是第一个可见的 TCP/IP 提供程序，这使得此开关成为为 [WSK 地址系列](ws2def-h.md)打开套接字的应用程序的默认选项。

 

