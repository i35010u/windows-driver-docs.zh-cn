---
title: 安装中间驱动程序
description: 安装中间驱动程序
ms.assetid: 75e299d0-b708-411d-9d37-609c8bf621f8
keywords:
- 中间驱动程序 WDK 网络，安装
- NDIS 中间驱动程序 WDK，安装
- 安装 NDIS 中间驱动程序 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5554f47851c6c3473795d782bc2f6b3a8e134a92
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212177"
---
# <a name="installing-an-intermediate-driver"></a>安装中间驱动程序





中间驱动程序需要两个 INF 文件。 其中一个 INF 文件定义了协议下边缘的安装参数。 另一个 INF 文件定义虚拟小型端口上边缘的安装参数。

协议 INF 文件是主 INF 文件。 安装协议下限后，将根据对协议 INF 文件中定义的微型端口驱动程序 INF 文件的引用安装虚拟小程序上边缘。

在 Windows Vista 上，你可以使用通知对象或自定义安装应用程序将微型端口驱动程序 INF 文件复制到系统 INF 目录。 对于 Windows Vista 和更高版本的操作系统版本，你应该使用协议 INF 文件中的 [**INF CopyINF 指令**](../install/inf-copyinf-directive.md) 复制微型端口驱动程序 INF 文件。 有关通知对象和复制 INF 文件的详细信息，请参阅 [中间驱动程序通知对象](intermediate-driver-notify-object.md)。

对于筛选器中间驱动程序，系统提供的设备安装程序类和用于 MUX 中间驱动程序的**NetTrans**都是**空间**。 虚拟微型端口的驱动程序类始终是 **网络**。

除 INF 文件外，还必须提供包含 MUX 中间驱动程序的通知对象。 对于筛选器中间驱动程序，通知对象是可选的。

虚拟微型端口设备始终使用 **ExcludeFromSelect** 指令从用户界面中删除。 因此，用户只会看到协议，并从协议 INF 文件安装协议。

**注意**   **ExcludeFromSelect**指令不会从 "**连接**" 对话框中删除虚拟设备。 但是，" \_ 微型端口驱动程序 INF 文件 *DDInstall* " 部分的 " **特征** " 条目中的 NCF 隐藏标志可防止虚拟小型端口显示在用户界面的任何部分（包括 " **连接** " 对话框）中。

 

本部分提供有关中间 INF 文件和通知对象的信息。 以下主题对此信息进行了说明：

[中间驱动程序 UpperRange 和 LowerRange INF 文件项](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)

[MUX 中间驱动程序安装](mux-intermediate-driver-installation.md)

[中间驱动程序通知对象](intermediate-driver-notify-object.md)

 

