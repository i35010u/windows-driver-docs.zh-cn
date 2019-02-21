---
title: AVStream 概述
description: AVStream 概述
ms.assetid: 305039fe-0a00-4f3e-ae1a-61c50a2f2fb3
keywords:
- AVStream WDK，有关 AVStream 微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd544857b853011b524d23d4bd1eff40d2f06cba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522818"
---
# <a name="avstream-overview"></a>AVStream 概述





AVStream 是由 Microsoft 提供多媒体类驱动程序，支持仅视频流式处理和集成音频/视频流式处理。 Microsoft 中导出驱动程序的操作系统的一部分提供 AVStream *Ks.sys*。 硬件供应商编写下运行的微型驱动程序*Ks.sys*。

音频驱动程序的首选的类驱动程序是由 Microsoft 提供音频[port 类](https://msdn.microsoft.com/library/windows/hardware/ff536829)驱动程序。 音频的供应商应该记下运行的微型驱动程序*Portcls.sys*。

Microsoft 支持[流式传输类](https://msdn.microsoft.com/library/windows/hardware/ff568275)仅对现有微型驱动程序的驱动程序。

AVStream 驱动程序生成 Microsoft Windows XP、 Microsoft Windows Server 2003、 或任何平台 Windows 98 金级或更高版本的 DirectX 8.0 或更高版本安装的版本。

如果你在上构建操作系统早于 Windows XP，请确保使用最新可用 DirectX 驱动程序开发工具包 (DDK)。 DirectX 9.0 AVStream、 内核流式处理组件和流类包含更新。

AVStream 到由供应商提供了明显的优点：

-   需要微型驱动程序编写器以生成更少的代码。

-   提供统一的内核流式处理音频和视频的微型驱动程序的类模型。

-   提供对供应商编写用户模式下插件的支持。这些是 COM 接口，提供用于访问属性值的方法。 你可以提供插件，而无需更改现有的微型驱动程序二进制文件。 有关详细信息，请参阅[内核流式处理代理插件](kernel-streaming-proxy-plug-ins-design-guide.md)。

在 AVStream 驱动程序模型中，供应商提供进行交互的微型驱动程序与 Microsoft 提供的类的驱动程序，如以下关系图中所示：

![说明在 avstream 和 ks 服务之间的关系的关系图](images/avstream.png)

 

 




