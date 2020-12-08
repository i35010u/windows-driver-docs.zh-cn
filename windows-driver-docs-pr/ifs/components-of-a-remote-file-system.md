---
title: 远程文件系统的组件
description: 远程文件系统的组件
keywords:
- 网络重定向 WDK，远程文件系统
- 重定向程序驱动程序 WDK，远程文件系统
- 远程文件系统 WDK
- 文件系统驱动程序 WDK，远程文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6171c378b64537962c85f445e6a265dc9a5c53c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786841"
---
# <a name="components-of-a-remote-file-system"></a>远程文件系统的组件


## <span id="ddk_components_of_a_remote_file_system_if"></span><span id="DDK_COMPONENTS_OF_A_REMOTE_FILE_SYSTEM_IF"></span>


实现远程文件系统需要以下基本元素：

-   安装在客户端上的网络重定向程序软件。

-   用于通信的定义完善的传输协议。

-   服务器上安装的文件服务器软件。

例如，Microsoft 网络远程文件系统的实现方式如下：

-   Microsoft 网络的客户端软件提供客户端网络重定向程序组件。

-   常见的 Internet 文件系统 (CIFS) ，它也称为服务器消息块 (SMB) 协议，用于定义用于通信的网络传输协议。

-   LAN Manager 服务器 (有时称为 SMB 服务器) 提供文件服务器服务。

安装在客户端上的网络重定向程序软件包含多个软件组件，一些软件组件在用户模式下运行，某些组件在内核模式下运行。

