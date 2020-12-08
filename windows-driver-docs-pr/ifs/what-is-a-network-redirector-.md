---
title: 什么是网络重定向程序
description: 什么是网络重定向程序
keywords:
- 网络重定向 WDK，关于网络重定向器
- 重定向程序驱动程序 WDK，关于网络重定向器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0a13ab8024cf6b431962535fddbdcffedba1009
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841261"
---
# <a name="what-is-a-network-redirector"></a>什么是网络重定向程序？


## <span id="ddk_what_is_a_network_redirector_if"></span><span id="DDK_WHAT_IS_A_NETWORK_REDIRECTOR_IF"></span>


网络重定向程序包含安装在客户端计算机上的软件组件，这些组件用于访问 (打印机和绘图仪的文件和其他资源，例如在远程系统上) 。 网络重定向程序将从本地客户端应用程序执行的文件操作) 请求发送 (或重定向到处理请求的远程服务器。 网络重定向程序从远程服务器接收响应，然后返回到本地应用程序。 网络重定向程序软件在客户端系统上创建远程文件和资源与本地文件和资源相同的外观，并允许以相同方式使用和操作它们。

对于本地客户端应用程序，网络重定向程序尝试使远程资源的访问尽可能透明。 如果出现网络问题，则可能会多次重试该请求，然后网络重定向程序会放弃并向客户端应用程序返回错误。

本部分包括以下主题：

[网络重定向程序的基本体系结构](basic-architecture-of-a-network-redirector.md)

 

 




