---
title: AVStream 概述
description: AVStream 概述
ms.assetid: 305039fe-0a00-4f3e-ae1a-61c50a2f2fb3
keywords:
- AVStream WDK，关于 AVStream 微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f5fe45f865f4c08dc04a458f61e3d478f2e8f67
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845284"
---
# <a name="avstream-overview"></a>AVStream 概述





AVStream 是 Microsoft 提供的多媒体类驱动程序，支持仅视频流式处理和集成音频/视频流式处理。 Microsoft 在导出驱动程序*Ks*的操作系统中提供 AVStream。 硬件供应商编写在*Ks*下运行的微型驱动程序。

音频驱动程序的首选类驱动程序是 Microsoft 提供的音频[端口类](https://docs.microsoft.com/windows-hardware/drivers/audio/introduction-to-port-class)驱动程序。 音频供应商应该编写在*Portcls*下运行的微型驱动程序。

Microsoft 仅支持现有微型驱动程序的[流类](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)驱动程序。

AVStream 驱动程序在 Microsoft Windows XP、Microsoft Windows Server 2003 或安装了 DirectX 8.0 或更高版本的任何平台 Windows 98 黄金或更高版本上生成。

如果是在 Windows XP 之前的操作系统上构建的，请确保使用最新的可用 DirectX 驱动程序开发工具包（DDK）。 DirectX 9.0 包含 AVStream、内核流式处理组件和 stream 类的更新。

AVStream 通过以下方式为供应商提供显著的优势：

-   需要微型驱动程序编写器来生成较少的代码。

-   为音频和视频微型驱动程序提供统一的内核流式处理类模型。

-   提供对供应商编写用户模式插件的支持。这些是提供访问属性值的方法的 COM 接口。 可以提供插件而无需更改现有的微型驱动程序二进制文件。 有关详细信息，请参阅[内核流式处理代理插件](kernel-streaming-proxy-plug-ins-design-guide.md)。

在 AVStream 驱动程序模型中，供应商提供与 Microsoft 提供的类驱动程序交互的微型驱动程序，如下图所示：

![说明 avstream 和 ks 服务之间的关系的关系图](images/avstream.png)

 

 




