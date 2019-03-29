---
title: 什么是网络重定向程序
description: 什么是网络重定向程序
ms.assetid: 5c966d92-7796-4cba-a90e-8c83240655ce
keywords:
- 网络重定向程序 WDK，有关网络重定向程序
- 有关网络重定向程序重定向程序驱动程序 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be38f977df4a49dd7ecfcad4aa71472fae169717
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577195"
---
# <a name="what-is-a-network-redirector"></a>什么是网络重定向程序？


## <span id="ddk_what_is_a_network_redirector_if"></span><span id="DDK_WHAT_IS_A_NETWORK_REDIRECTOR_IF"></span>


网络重定向程序包含用于访问文件和远程系统上的其他资源 （打印机和绘图仪，例如） 的客户端计算机上安装的软件组件。 网络重定向程序发送 （或将重定向） 从本地客户端应用程序到在其中处理请求的远程服务器的文件操作的请求。 网络重定向程序接收来自远程服务器，然后返回到本地应用程序的响应。 网络重定向程序软件创建外观客户端系统上的远程文件和资源是相同的作为本地文件和资源，并允许他们可以使用和操作方式相同。

网络重定向程序尝试对远程资源访问进行尽可能本地客户端应用程序透明。 如果出现网络问题，该请求可能会重试几次网络重定向程序将放弃运行，并将错误返回到客户端应用程序之前。

本部分包括以下主题：

[网络重定向程序的基本体系结构](basic-architecture-of-a-network-redirector.md)

 

 




