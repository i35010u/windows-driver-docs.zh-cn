---
title: 初始化 SAN 服务提供程序
description: 初始化 SAN 服务提供程序
ms.assetid: 73e923e9-c7bd-4d46-9d21-fc1392a79c65
keywords:
- Windows 套接字直接 WDK，初始化 SAN 使用率
- 初始化 SAN 使用率
- SAN 服务提供商 WDK，初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2706dc2af4c4a519705b69e1dcddc980bdcd1287
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381334"
---
# <a name="initializing-a-san-service-provider"></a>初始化 SAN 服务提供程序





下图中所述，Windows 套接字交换机初始化 SAN 服务提供程序。

![说明 windows 套接字交换机如何初始化系统区域网络 (san) 服务提供商的关系图 ](images/apiflow1.png)

Windows 加载 Windows 套接字切换到应用程序的进程的 DLL 后，会发生以下事件序列。

**若要初始化 SAN 服务提供程序**

1.  开关检测到和加载 TCP/IP 提供程序，然后查询的 SAN 服务提供商在注册表中检测到所有这些提供程序列表中所述[SAN 服务提供程序安装](installing-a-san-service-provider.md)。 此开关调用每个检测到提供程序[ **WSPStartupEx** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566321(v=vs.85))函数以开始使用该提供程序。

2.  在中**WSPStartupEx**调用，该交换机将传递一个指向[ **WSAPROTOCOL\_INFOW** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565963(v=vs.85))结构，其中包含 TCP/IP 提供程序的协议信息。 TCP/IP 提供程序的协议指示 SAN 服务提供程序，它已初始化由交换机，而不是由其他分层的服务提供程序或 Windows 套接字接口。 开关将作为 Windows 套接字的服务提供程序接口 (SPI) 部分中的 Microsoft Windows SDK 文档中的建议传递 TCP/IP 提供程序的协议信息而不是 SAN 服务提供商的传输信息。

    由于 SAN 服务提供商可以检测到由该交换机初始化，它可以公开相应的一组到交换机的入口点函数。 如果 SAN 服务提供程序由应用程序直接进行初始化，它可以公开另一组到该应用程序的入口点函数。 如果 SAN 服务提供商进行了分层下开关，该提供程序必须遵守的扩展和在本部分中所述的行为。

3.  SAN 服务提供商的代理驱动程序将获取列表中所述分配给其控制下的每个 NIC 的 IP 地址[注册 SAN NIC 通知](registering-for-san-nic-notifications.md)。 SAN 服务提供程序使用的专用接口从其代理驱动程序检索此列表。 此开关调用 SAN 服务提供商[ **WSPSocket** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566319(v=vs.85))函数来创建套接字。 此开关使用此套接字来检索分配给 SAN 服务提供商的代理驱动程序的控制下的 Nic 的 IP 地址的完整列表。 切换检索此列表中所述[接收和转换 NIC 地址](receiving-and-translating-nic-addresses.md)。 根据此列表和其他 SAN 服务提供商的列表，此开关生成映射到 SAN 服务提供程序的本地 IP 子网的表。

4.  Windows 套接字交换机必须检索扩展 Windows 套接字服务提供程序接口 (SPI) 使用的 SAN 服务提供商的入口点函数的指针与 San。 若要检索每个这些扩展功能，Windows 套接字开关调用 SAN 服务提供商[ **WSPIoctl** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff566296(v=vs.85))函数，并将传递 SIO\_获取\_扩展\_函数\_指针命令代码以及其值标识其中一种 GUID 扩展函数。

    有关这些函数的完整说明，请参阅[Windows 套接字的 SPI 扩展 San](windows-sockets-spi-extensions-for-sans.md)。

5.  此开关可以创建线程来支持也非阻止侦听套接字连接请求，如中所述[设置 SAN 连接](setting-up-a-san-connection.md)。

 

 





