---
title: 网络重定向程序的基本体系结构
description: 网络重定向程序的基本体系结构
ms.assetid: 60a7c79d-b89f-4c8b-9619-bd48c9e1efac
keywords:
- 网络重定向 WDK，体系结构
- 重定向程序驱动程序 WDK、体系结构
- TDI 驱动程序 WDK 文件系统
- 传输驱动程序接口 WDK 文件系统
- Dll WDK 文件系统
- SYS WDK 文件系统
- 内核模式文件系统驱动程序 WDK 文件系统
- 用户模式 Dll WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 250bd3f64cd0196e8e25dd2cadae5fc98939c780
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841490"
---
# <a name="basic-architecture-of-a-network-redirector"></a>网络重定向程序的基本体系结构


## <span id="ddk_basic_architecture_of_a_network_redirector_if"></span><span id="DDK_BASIC_ARCHITECTURE_OF_A_NETWORK_REDIRECTOR_IF"></span>


以下基本软件组件是网络重定向程序的一部分所必需的：

-   提供网络重定向程序功能的内核模式文件系统设备驱动程序（SYS）。

-   一种用户模式的动态链接库（DLL），它为客户端用户应用程序提供对非文件操作的网络提供程序接口的访问权限，并启用与提供网络重定向程序功能的内核模式文件系统驱动程序的通信。

网络重定向程序的内核模式文件系统驱动程序组件与对象管理器、缓存管理器、内存管理器、i/o 系统和其他内核系统交互，以便将远程文件访问集成到操作系统中。 驱动程序通过用于远程文件访问的 i/o 管理器接收来自客户端应用程序的请求，并通过网络将必要的信息发送到远程文件服务器。 驱动程序还会接收来自远程文件服务器的响应，并通过 i/o 管理器将信息传递回客户端应用程序。 网络重定向程序驱动程序还必须实现用于远程访问的网络协议，或者提供对另一核心驱动程序、用户模式应用程序或实现此网络协议或通信机制的服务的调用。 实现此网络通信的最常见方法是使用传输驱动程序接口（TDI）来调用现有的网络协议堆栈（例如 TCP/IP）。 然后，网络协议堆栈会将网络驱动程序接口规范（NDIS）用于网络接口卡，以底部进行通信。 对于此通信机制，还可以使用特定于应用程序的接口。

用户模式 DLL 通过不是文件操作的网络提供程序接口接收来自客户端的特殊请求。 这些请求可用于确定网络提供商的功能，枚举远程网络资源，登录到远程网络，更改网络密码，与远程服务器连接，装载远程网络共享或资源，以及正在从远程共享断开连接。 用户模式 DLL 实现了等效的 WNet 用户模式 Api 来访问远程文件系统。 然后，此 DLL 通过特殊的 IOCTL 调用与内核模式网络重定向器驱动程序通信以满足这些客户端请求。 例如，枚举网络资源（浏览网络邻居）时或连接到远程文件共享和资源（打印机）时，Windows 资源管理器会调用此 DLL。 还会从 NET 命令行工具调用此 DLL，以查看远程资源（**net view** \\\\*computername*），并连接或断开与远程文件共享（**net use**）的连接或断开连接。 自定义应用程序也可以使用多提供商路由器的公开 WNet Api （MPR）调用此 DLL。

网络重定向程序可能还需要多个其他组件：

-   如果需要将任何全局数据表安全地存储在用户模式 DLL 中，则服务应用程序可能需要充当用户模式 DLL 和内核模式驱动程序之间的中介。 由于在客户端应用程序的进程空间中实例化用户模式 DLL，因此无法保护所有需要在所有客户端应用程序中全局的内部数据表。 连接到用户模式网络提供程序 DLL 时，可以将每个客户端的数据专用于每个客户端应用程序，但不能包含全局数据。 服务应用程序（.exe 文件）可用作用户模式 DLL 和存储全局数据表的内核驱动程序之间的中介。 例如，Microsoft 网络使用 svchost.exe 中内置的工作站服务来存储 "net use" 连接的全局表，并充当内核模式驱动程序的中介。 对于 Microsoft 网络，用户模式 DLL ntlanman 调用了 svchost.exe 中的 Workstation 服务，后者随后调用内核模式驱动程序 mrxsmb，后者提供网络重定向程序功能。

-   用于在系统中安装和正确注册网络重定向程序组件的系统，必须包括创建任何必需的注册表项。 如果不再需要该软件，还应提供用于卸载网络重定向器的方法。 可以使用 Microsoft 系统安装程序（MSI）或 Windows INF 脚本文件来执行此设置。 此安装和设置也可以使用自定义安装程序来完成。

-   如果网络重定向器使用的网络协议未包含在操作系统中（例如 Xerox 网络服务），则需要安装自定义内核模式 TDI 驱动程序。 需要安装新的 TDI 驱动程序来实现用于通信的网络协议。 内核模式网络重定向程序驱动程序连接到自定义 TDI 驱动程序的上边缘。 自定义 TDI 驱动程序将使用 NDIS 驱动程序在其下边缘进行通信。

    请注意，如果网络重定向器使用 TCP/IP 协议，则不需要自定义 TDI 驱动程序。 在这种情况下，网络重定向程序将连接到 TCP/IP 协议 TDI 驱动程序的上边缘。

-   有时需要使用管理工具将用户模式的访问权限提供给内核模式驱动程序，以便进行特殊配置、诊断和管理。 此工具还可用于启用或禁用跟踪和日志记录，以解决问题。 该工具使用各种自定义专用 IOCTLs 与内核驱动程序通信。 此工具还可以提供对服务控制管理器（SCM）的访问权限，以管理中间服务，在该服务中，全局数据将安全地存储在用户模式的网络提供程序 DLL 中。

**请注意**，在 Windows Vista 之后的 Microsoft windows 版本中不支持   TDI。 请改用[Windows 筛选平台](https://docs.microsoft.com/windows-hardware/drivers/network/windows-filtering-platform-callout-drivers2)或[Winsock 内核](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)。

 

 

 




