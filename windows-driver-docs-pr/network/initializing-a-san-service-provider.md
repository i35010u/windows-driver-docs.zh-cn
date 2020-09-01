---
title: 初始化 SAN 服务提供程序
description: 初始化 SAN 服务提供程序
ms.assetid: 73e923e9-c7bd-4d46-9d21-fc1392a79c65
keywords:
- Windows 套接字直通 WDK，初始化 SAN 使用情况
- 正在初始化 SAN 使用情况
- SAN 服务提供商 WDK，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a90cc80b4c426f88c5cfd42e7cba2ac30a0cff67
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217282"
---
# <a name="initializing-a-san-service-provider"></a>初始化 SAN 服务提供程序





Windows 套接字交换机按下图所述初始化 SAN 服务提供程序。

![说明 windows 套接交换机如何初始化系统区域网络 (san) 服务提供商的关系图 ](images/apiflow1.png)

在 Windows 将 Windows 套接字开关 DLL 加载到应用程序的进程中后，将发生以下事件序列。

**初始化 SAN 服务提供程序**

1.  交换机检测并加载 TCP/IP 提供程序，然后在注册表中查询 SAN 服务提供程序的列表以检测所有这些提供程序，如 [安装 SAN 服务提供程序](installing-a-san-service-provider.md)中所述。 开关调用检测到的每个提供程序的 [**WSPStartupEx**](/previous-versions/windows/hardware/network/ff566321(v=vs.85)) 函数，以启动使用该提供程序。

2.  在 **WSPStartupEx** 调用中，开关传递指向包含 tcp/ip 提供程序的协议信息的 [**WSAPROTOCOL \_ INFOW**](/previous-versions/windows/hardware/network/ff565963(v=vs.85)) 结构的指针。 TCP/IP 提供程序的协议向 SAN 服务提供程序指示它已由交换机（而不是其他分层服务提供程序或 Windows 套接字接口）初始化。 开关传递 TCP/IP 提供程序的协议信息，而不是 SAN 服务提供程序的传输信息，如 Microsoft Windows SDK 文档 (SPI) 部分中所建议的那样。

    由于 SAN 服务提供程序可以检测到它已被交换机初始化，因此它可以向开关公开适当的入口点函数集。 如果 SAN 服务提供程序由应用程序直接初始化，它可以向该应用程序公开另一组入口点函数。 如果 SAN 服务提供程序在交换机下分层，则该提供程序必须遵守此部分中所述的扩展和行为。

3.  SAN 服务提供商的代理驱动程序获取分配给其控件下的每个 NIC 的 IP 地址列表，如 [注册 SAN NIC 通知](registering-for-san-nic-notifications.md)中所述。 SAN 服务提供程序使用专用接口从其代理驱动程序检索此列表。 开关调用 SAN 服务提供程序的 [**WSPSocket**](/previous-versions/windows/hardware/network/ff566319(v=vs.85)) 函数来创建套接字。 交换机使用此套接字来检索分配给 Nic 的 IP 地址的完整列表，该列表是在控制 SAN 服务提供程序的代理驱动程序的控制下的。 开关将检索此列表，如 [接收和转换 NIC 地址](receiving-and-translating-nic-addresses.md)中所述。 根据此列表以及其他 SAN 服务提供商的列表，该交换机会构建一个将本地 IP 子网映射到 SAN 服务提供商的表。

4.  Windows 套接字交换机必须检索指向 SAN 服务提供商入口点函数的指针，这些函数将 Windows 套接字服务提供程序接口扩展 (SPI) 以便与 San 一起使用。 为了检索这些扩展函数中的每一个，Windows 套接字开关都调用一个 SAN 服务提供程序的 [**WSPIoctl**](/previous-versions/windows/hardware/network/ff566296(v=vs.85)) 函数，并传递 SIO \_ 获取 \_ 扩展 \_ 函数 \_ 指针命令代码以及其值标识这些扩展函数之一的 GUID。

    有关这些函数的完整说明，请参阅 [适用于 san 的 Windows 套接 SPI 扩展](windows-sockets-spi-extensions-for-sans.md)。

5.  如 [设置 SAN 连接](setting-up-a-san-connection.md)中所述，开关可以创建线程以支持侦听套接字和非阻止连接请求。

 

