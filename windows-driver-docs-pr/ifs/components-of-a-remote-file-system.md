---
title: 远程文件系统的组件
description: 远程文件系统的组件
ms.assetid: b2cd153a-5bcc-4670-8542-afa55e14727a
keywords:
- 网络重定向程序 WDK，远程文件系统
- 重定向程序驱动程序 WDK，远程文件系统
- 远程文件系统 WDK
- 文件系统驱动程序 WDK，远程文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a25f729727580b04a5f25d16fe625449b62d1d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568406"
---
# <a name="components-of-a-remote-file-system"></a>远程文件系统的组件


## <span id="ddk_components_of_a_remote_file_system_if"></span><span id="DDK_COMPONENTS_OF_A_REMOTE_FILE_SYSTEM_IF"></span>


实现远程文件系统所需的以下基本元素：

-   安装在客户端的网络重定向程序软件。

-   明确定义的传输协议，用于进行通信。

-   在服务器上安装的文件服务器软件。

例如，按如下所示实现 Microsoft 网络的远程文件系统：

-   Microsoft 网络软件的客户端提供客户端网络重定向程序组件。

-   常见的 Internet 文件系统 (CIFS)，这也称为服务器消息块 (SMB) 协议，定义用于通信的网络传输协议。

-   LAN 管理器服务器 （有时称为 SMB 服务器） 提供了文件服务器服务。

在客户端上安装的网络重定向程序软件包括几个软件组件，一些在用户模式下操作和一些在内核模式下操作。

以下各节讨论非常重要的开发人员的 Windows Server 2003、 Windows XP 和 Windows 2000 上的远程文件系统的概念。 论述了以下主题：

[网络重定向程序简介](introduction-to-network-redirectors.md)

[内核网络重定向程序驱动程序组件](kernel-network-redirector-driver-components.md)

 

 




