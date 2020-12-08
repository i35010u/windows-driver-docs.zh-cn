---
title: AVStream 概述
description: AVStream 概述
keywords:
- AVStream WDK，关于 AVStream 微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcac3954d334980c44b7528eb9a9e3c820e59080
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786649"
---
# <a name="avstream-overview"></a>AVStream 概述





AVStream 是 Microsoft 提供的多媒体类驱动程序，支持仅视频流式处理和集成音频/视频流式处理。 Microsoft 在 *Ks.sys* 导出驱动程序的操作系统中提供 AVStream。 硬件供应商编写在 *Ks.sys* 下运行的微型驱动程序。

音频驱动程序的首选类驱动程序是 Microsoft 提供的音频 [端口类](../audio/introduction-to-port-class.md) 驱动程序。 音频供应商应该编写在 *Portcls.sys* 下运行的微型驱动程序。

Microsoft 仅支持现有微型驱动程序的 [流类](/windows-hardware/drivers/ddi/_stream/index) 驱动程序。

AVStream 驱动程序在 Microsoft Windows XP、Microsoft Windows Server 2003 或安装了 DirectX 8.0 或更高版本的任何平台 Windows 98 黄金或更高版本上生成。

如果是在 Windows XP 之前的操作系统上构建的，请确保使用最新的可用 DirectX 驱动程序开发工具包 (DDK) 。 DirectX 9.0 包含 AVStream、内核流式处理组件和 stream 类的更新。

AVStream 通过以下方式为供应商提供显著的优势：

-   需要微型驱动程序编写器来生成较少的代码。

-   为音频和视频微型驱动程序提供统一的内核流式处理类模型。

-   提供对供应商编写用户模式插件的支持。这些是提供访问属性值的方法的 COM 接口。 可以提供插件而无需更改现有的微型驱动程序二进制文件。 有关详细信息，请参阅 [内核流式处理代理插件](kernel-streaming-proxy-plug-ins-design-guide.md)。

在 AVStream 驱动程序模型中，供应商提供与 Microsoft 提供的类驱动程序交互的微型驱动程序，如下图所示：

![说明 avstream 和 ks 服务之间的关系的关系图](images/avstream.png)

 

