---
title: 远程文件系统简介
description: 远程文件系统简介
keywords:
- 网络重定向 WDK，远程文件系统
- 重定向程序驱动程序 WDK，远程文件系统
- 远程文件系统 WDK
- 文件系统驱动程序 WDK，远程文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6eb05c04c00997ec2a7a9864552cdc4999343acb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830573"
---
# <a name="introduction-to-remote-file-systems"></a>远程文件系统简介


## <span id="ddk_introduction_to_remote_file_systems_if"></span><span id="DDK_INTRODUCTION_TO_REMOTE_FILE_SYSTEMS_IF"></span>


远程文件系统使在客户端计算机上运行的应用程序能够访问存储在其他计算机上的文件。 远程文件系统还经常 (远程打印机提供其他资源，例如) 可从客户端计算机进行访问。 远程文件和资源访问使用某种形式的局域网 (LAN) 、广域网 (WAN) 、点到点链接或其他通信机制进行。 这些文件系统通常称为网络文件系统或分布式文件系统。

Microsoft 网络是 Windows Server 2003、Windows XP 和 Windows 2000 中包含的本机远程文件系统。 Microsoft 网络提供对文件的远程访问以及对远程打印机和绘图仪的访问。 Microsoft 网络在早期版本的 Windows 网络流入量称为 LAN Manager。

Microsoft 还包括对 Windows 上其他一些远程文件系统的支持：

-   NetWare Core 协议 (NCP) 

-   WebDAV (使用远程 web 服务器的文件访问) 

-   AppleTalk 文件和打印机共享 (支持从 Macintosh 客户端连接到运行 Windows Server 2003 和 Windows 2000 Server) 的系统

-   网络文件系统 (NFS)

-   Microsoft Host Integration Server 2000 随附的 IBM 大型机 VSAM 和 AS/400 文件访问

**注意**  在 Windows Server 2003 R2 之前的 Windows 操作系统版本中，你可以通过安装适用于 UNIX 的 Microsoft 服务来获取 NFS。 对于 Windows Server 2003 R2 及更高版本的 Windows 操作系统，NFS 作为可选的 Windows 组件包含在内。

 

远程文件系统是由软件组件的集合实现的。 所需软件组件的数量和复杂性因远程文件系统的设计和复杂性而异。

客户端系统上的软件提供远程文件和资源访问权限。 此客户端软件充当 "网络重定向程序"，用于将文件操作的本地调用转发给某些远程服务器。 此网络重定向器使远程资源显示为本地资源。

服务器系统上的软件实现远程文件服务器操作，这些操作可访问服务器上的本地文件存储或资源。 从文件服务器上处理的客户端网络重定向程序收到请求，并将响应发送回客户端。

系统可以同时充当某些系统的客户端，也可以充当其他客户端的服务器。 因此，通常会发现在单个系统上运行的客户端和服务器软件。

本节包含下列主题：

[远程文件系统的组件](components-of-a-remote-file-system.md)

 

 




