---
title: 安装 SAN 服务提供程序
description: 安装 SAN 服务提供程序
ms.assetid: 3a7fcacf-ef26-4a41-a991-230daf67accf
keywords:
- Windows 套接字直接 WDK、 安装组件
- SAN 服务提供商 WDK，安装
- SAN 服务提供商 WDK，注册
- 注册 SAN 服务提供商
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce3cd2703ea3499a666caa6665b9a88f33237f54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382206"
---
# <a name="installing-a-san-service-provider"></a>安装 SAN 服务提供程序





SAN 服务提供商通常会安装与 Windows 套接字交换机的接口的基本 Windows 套接字服务提供程序。 尽管 SAN 服务提供商可供直接使用由安装应用程序相反，Windows 套接字直接技术不支持以这种方式使用 SAN 服务提供程序。 安装应用程序直接使用的 SAN 服务提供商将导出其本机地址系列和协议特征，而不是那些 TCP/IP 协议。

间接公开给应用程序通过 Windows 套接字交换机 SAN 服务提供商必须设置 PFL\_中的隐藏标志**dwProviderFlags** SAN 服务提供商的成员[ **WSAPROTOCOL\_INFOW** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff565963(v=vs.85))结构。 若要在操作系统上安装 SAN 服务提供商，SAN 服务提供商的安装机制将传递此结构在调用**WSCInstallProvider**函数。 有关详细信息**WSCInstallProvider**，请参阅 Microsoft Windows SDK 文档。 SAN 服务提供商的安装机制可能会为例，安装程序或函数导出由 SAN 服务提供程序和由 INF file 指令调用。

SAN 服务提供商的安装机制必须添加值为类型 REG\_二进制到以下注册表项的前 SAN 服务提供商可以检测到的 Windows 套接字切换作为基本的 Windows 套接字服务提供程序：

```Console
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Winsock\
Parameters\TCP on SAN
```

此值包含中的值的二进制表示形式**ProviderId** WSAPROTOCOL 成员\_INFOW 结构。 此值 SAN 服务提供程序注册到 Windows 套接字开关。 此成员包含供应商的 SAN 服务提供程序分配的全局唯一标识符 (GUID)。

供应商还可以指定唯一的名称，表示此 GUID，例如：

-   商标字的产品名称

-   唯一数字值

-   GUID 的文本表示形式

**若要注册 SAN 服务提供程序**

1.  交换机调用**WSAProviderConfigChange**函数来检测 Windows 套接字提供程序安装和删除事件。

2.  安装新的 Windows 套接字服务提供程序后，此开关调用**WSCEnumProtocols**函数来查询 Windows 套接字目录和 SAN 服务提供程序的列表在注册表中以确定是否在新服务提供程序控制 SAN。 有关详细信息**WSCEnumProtocols**，请参阅 Windows SDK。

3.  如果交换机检测到新 SAN 服务提供程序，该交换机初始化该服务提供程序中所述[初始化 SAN 服务提供商](initializing-a-san-service-provider.md)。

4.  开关也调用新安装的 SAN 服务提供程序的以下函数，SAN 服务提供程序初始化到任何现有的侦听套接字绑定到通配符 IP 地址 (0.0.0.0) 的服务后 (通配符 IP 地址意味着 SAN服务提供程序应接受传入连接请求从其控制的所有 Nic）：

    <a href="" id="wspsocket"></a>**WSPSocket**  
    创建的套接字

    <a href="" id="wspbind"></a>**WSPBind**  
    将套接字绑定到通配符 IP 地址

    <a href="" id="wsplisten"></a>**WSPListen**  
    设置要确认和队列的传入连接的套接字请求直到接受由交换机

    **请注意**  从 Windows Vista 开始，通配符 IP 地址 0.0.0.0 不可用。
    如果还从 Windows Vista **IPAutoconfigurationEnabled**注册表项设置为值为 0，禁用自动 IP 地址分配，和任何 IP 地址分配。 在这种情况下， **ipconfig**命令行工具将不会显示一个 IP 地址。 如果项设置为非零值，自动分配 IP 地址。 此密钥也可位于注册表中的以下路径：

    **HKEY\_本地\_MACHINE\\系统\\当前控件集\\Services\\Tcpip\\参数\\IPAutoconfigurationEnabled**

    **HKEY\_本地\_MACHINE\\系统\\当前控件集\\Services\\Tcpip\\参数\\接口\\*GUID*\\IPAutoconfigurationEnabled**

     

 

 





