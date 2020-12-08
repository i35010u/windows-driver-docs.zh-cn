---
title: 点选打印简介
description: 点选打印简介
keywords:
- 指向和打印 WDK，关于点和打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5dd20b47e3b3a3475b696b637357bb302a85153
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835637"
---
# <a name="introduction-to-point-and-print"></a>点选打印简介





"*指向和打印*" 是指允许 Windows 2000 和更高版本客户端上的用户创建到远程打印机的连接，而不提供磁盘或其他安装媒体的一项功能。 所有必需的文件和配置信息会自动从打印服务器下载到客户端。

点和打印技术提供了两种方法，通过这些方法可以指定应从打印服务器发送到客户端计算机的文件：

-   文件可以与打印机驱动程序相关联。 这些文件与使用该驱动程序的每个打印队列相关联。

-   文件可与单个打印队列关联。

有关详细信息，请参阅 [打印机安装过程中的支持点和打印](supporting-point-and-print-during-printer-installations.md)。

用户应用程序调用 **AddPrinterConnection** 函数时 (Microsoft Windows SDK 文档) 中所述的设置打印机连接时，将执行以下操作：

-   与驱动程序相关联的文件和与队列关联的文件将从打印服务器下载到客户端。

-   打印机的注册表中存储在服务器的注册表中的配置参数的当前值会下载到客户端。

有关详细信息，请参阅 [在打印机连接期间支持点和打印](supporting-point-and-print-during-printer-connections.md)。

 

 




