---
title: 远程文件系统简介
description: 远程文件系统简介
ms.assetid: 24fe7b8e-b956-4c27-be12-8317e4f35ba6
keywords:
- 网络重定向程序 WDK，远程文件系统
- 重定向程序驱动程序 WDK，远程文件系统
- 远程文件系统 WDK
- 文件系统驱动程序 WDK，远程文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4084d9f488f3b64977a4de09d3c7221540a09494
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568956"
---
# <a name="introduction-to-remote-file-systems"></a>远程文件系统简介


## <span id="ddk_introduction_to_remote_file_systems_if"></span><span id="DDK_INTRODUCTION_TO_REMOTE_FILE_SYSTEMS_IF"></span>


远程文件系统启用客户端计算机访问文件存储在另一台计算机上运行的应用程序。 远程文件系统通常还使其他资源 （例如远程打印机） 的客户端计算机可访问。 远程文件和资源访问权限会发生使用某种形式的局域网 (LAN)、 广域网 (WAN)、 点对点链路或其他通信机制。 这些文件系统通常称为网络文件系统或分布式的文件系统。

Microsoft 网络是 Windows Server 2003、 Windows XP 和 Windows 2000 中包含的本机远程文件系统。 Microsoft 网络提供对文件的远程访问以及对远程打印机和绘图仪的访问。 Microsoft 网络的 Windows 早期版本中调用 LAN 管理器网络。

Microsoft 还支持在 Windows 上的多个其他远程文件系统：

-   NetWare 核心协议 (NCP)

-   WebDAV （使用远程 web 服务器的文件访问）

-   AppleTalk 文件和打印机共享 （支持来自 Macintosh 客户端连接到运行 Windows Server 2003 和 Windows 2000 Server 的系统）

-   网络文件系统 (NFS)

-   IBM 大型机 VSAM 和 AS / 400 文件访问权限，包括与 Microsoft 主机集成服务器 2000年

**请注意**  在 Windows 操作系统，在 Windows Server 2003 R2 之前的版本中，你可以通过安装 Microsoft Services for UNIX 中获取 NFS。 使用 Windows Server 2003 R2 和更高版本的 Windows 操作系统，NFS 是作为一个可选的 Windows 组件包含在内。

 

远程文件系统由一系列软件组件实现。 数量和所需的软件组件的复杂性而异的设计和远程文件系统的复杂性。

客户端系统上的软件提供远程文件和资源访问权限。 此客户端软件作为"网络重定向程序"转发到某些远程服务器的文件操作的本地调用。 此网络重定向程序可以显示像是本地的远程资源。

服务器系统上的软件在服务器上实现远程文件服务器操作的访问本地文件存储或资源。 从客户端网络重定向程序在文件服务器上处理收到的请求和响应发送回客户端。

作为这两个客户端到某些系统和其他客户端到服务器，系统可以采取行动。 因此，很常见，以查找在单个系统上运行的客户端和服务器软件。

本部分包含以下主题：

[远程文件系统的组件](components-of-a-remote-file-system.md)

 

 




