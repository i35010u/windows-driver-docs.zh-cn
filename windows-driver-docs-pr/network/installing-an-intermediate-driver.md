---
title: 安装中间驱动程序
description: 安装中间驱动程序
ms.assetid: 75e299d0-b708-411d-9d37-609c8bf621f8
keywords:
- 中间驱动程序 WDK 网络安装
- NDIS 中间层驱动程序 WDK，安装
- 安装 NDIS 中间层驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 514232160158532356fecd69164da2af2e52d4fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382208"
---
# <a name="installing-an-intermediate-driver"></a>安装中间驱动程序





中间驱动程序需要两个 INF 文件。 其中一个 INF 文件定义协议下边缘的安装参数。 另一个 INF 文件定义虚拟微型端口上边缘的安装参数。

协议 INF 文件是主 INF 文件。 安装协议下边缘后，会安装虚拟微型端口上边缘，基于对微型端口驱动程序 INF 文件协议 INF 文件中定义的引用。

在 Windows Vista 中，可以使用通知对象或自定义安装应用程序将微型端口驱动程序 INF 文件复制到系统 INF 目录。 对于 Windows Vista 及更高版本的操作系统版本，应使用[ **INF CopyINF 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyinf-directive)协议 INF 文件要复制的微型端口驱动程序 INF 文件中。 通知对象和复制 INF 文件有关的详细信息，请参阅[中间驱动程序通知对象](intermediate-driver-notify-object.md)。

下边缘是的协议的系统提供的设备安装程序类**NetService**筛选器的中间驱动程序和**NetTrans** MUX 中间驱动程序。 虚拟微型端口驱动程序类是始终**Net**。

MUX 中间驱动程序时，除了 INF 文件中，您必须还提供通知对象。 通知对象是可选的筛选器中间驱动程序。

虚拟微型端口设备使用始终删除从用户界面**ExcludeFromSelect**指令。 因此，该用户只能查看协议，并从协议 INF 文件安装的协议。

**请注意**   **ExcludeFromSelect**指令不会删除从虚拟设备**连接**对话框。 但是，NCF\_微型端口驱动程序 INF 文件中的隐藏标志*DDInstall*部分中的**特征**条目可防止虚拟微型端口显示在用户的任何部分接口，包括**连接**对话框。

 

本部分提供有关中间 INF 文件的信息，并通知对象。 以下主题中描述了此信息：

[中间驱动程序 UpperRange 和 LowerRange INF 文件条目](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)

[MUX 中间驱动程序安装](mux-intermediate-driver-installation.md)

[中间驱动程序通知对象](intermediate-driver-notify-object.md)

 

 





