---
title: 安装 SAN 服务提供程序
description: 安装 SAN 服务提供程序
keywords:
- Windows Socket Direct WDK，安装组件
- SAN 服务提供商 WDK，安装
- SAN 服务提供商 WDK，注册
- 注册 SAN 服务提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86a5333190a8331fb9d5aed6cd13dfbac2cb0523
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795953"
---
# <a name="installing-a-san-service-provider"></a>安装 SAN 服务提供程序





SAN 服务提供商通常作为与 Windows 套接交换机交互的基本 Windows 套接字服务提供程序安装。 尽管可以安装 SAN 服务提供程序以供应用程序直接使用，但 Windows 套接字直接技术不支持以这种方式使用 SAN 服务提供程序。 安装为由应用程序直接使用的 SAN 服务提供程序将导出其本机地址族和协议特征，而不是 TCP/IP 协议。

通过 Windows 套接交换机间接公开给应用程序的 SAN 服务提供程序必须 \_ 在 san 服务提供商的 [**WSAPROTOCOL \_ INFOW**](/previous-versions/windows/hardware/network/ff565963(v=vs.85))结构的 **dwProviderFlags** 成员中设置 default.pfl 隐藏标志。 若要在操作系统上安装 SAN 服务提供程序，SAN 服务提供程序的安装机制会在对 **WSCInstallProvider** 函数的调用中传递此结构。 有关 **WSCInstallProvider** 的详细信息，请参阅 Microsoft Windows SDK 文档。 SAN 服务提供程序的安装机制可以是例如，安装程序或由 SAN 服务提供程序导出并由 INF 文件指令调用的函数。

SAN 服务提供程序的安装机制必须在注册表中将 REG BINARY 类型的值添加 \_ 到以下注册表项，然后 Windows 套接字交换机可以将 san 服务提供程序作为基本 Windows 套接字服务提供程序检测：

```Console
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Winsock\
Parameters\TCP on SAN
```

此值包含 WSAPROTOCOL INFOW 结构中 **ProviderId** 成员的值的二进制表示形式 \_ 。 此值向 Windows 套接交换机注册一个 SAN 服务提供程序。 此成员包含供应商分配给 SAN 服务提供商 (GUID) 全局唯一标识符。

供应商还可以分配代表此 GUID 的唯一名称，例如：

-   产品名称商标字

-   唯一的数值

-   GUID 的文本表示形式

**注册 SAN 服务提供程序**

1.  开关调用 **WSAProviderConfigChange** 函数来检测 Windows 套接字提供程序的安装和删除事件。

2.  安装新的 Windows 套接字服务提供程序后，交换机将调用 **WSCEnumProtocols** 函数来查询 Windows 套接 catalog，并在注册表中查询 san 服务提供商列表，以确定新的服务提供商是否控制 SAN。 有关 **WSCEnumProtocols** 的详细信息，请参阅 Windows SDK。

3.  如果交换机检测到新的 SAN 服务提供程序，则交换机会根据 [初始化 San 服务提供程序](initializing-a-san-service-provider.md)中所述初始化该服务提供程序。

4.  在对 SAN 服务提供程序进行初始化后，该开关还会调用新安装的 SAN 服务提供程序的以下功能，以便为绑定到通配符 IP 地址 (0.0.0.0)  () 的任何现有侦听套接字提供服务。

    <a href="" id="wspsocket"></a>**WSPSocket**  
    创建套接字

    <a href="" id="wspbind"></a>**WSPBind**  
    将套接字绑定到通配符 IP 地址

    <a href="" id="wsplisten"></a>**WSPListen**  
    将套接字设置为确认并将传入连接请求排队，直到交换机接受

    **注意**  从 Windows Vista 开始，通配符 IP 地址0.0.0.0 不可用。
    此外，从 Windows Vista 开始，如果 **IPAutoconfigurationEnabled** 注册表项设置为值0，将禁用自动 ip 地址分配，并且不分配 ip 地址。 在这种情况下， **ipconfig** 命令行工具不会显示 IP 地址。 如果将密钥设置为非零值，则会自动分配 IP 地址。 此密钥可位于注册表中的以下路径：

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ 当前控制集 \\ 服务 \\ Tcpip \\ 参数 \\ IPAutoconfigurationEnabled**

    **HKEY \_ 本地 \_ 计算机 \\ 系统 \\ 当前控制集 \\ 服务 \\ Tcpip \\ 参数 \\ 接口 \\ *GUID* \\ IPAutoconfigurationEnabled**

     

 

