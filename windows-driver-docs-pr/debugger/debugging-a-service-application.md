---
title: 调试服务应用程序
description: 调试服务应用程序
keywords:
- 服务应用程序调试
- 事后调试，调试服务应用程序
- services
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f00f4ee2e9460798cfbd97b7db04e34cec04018
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803633"
---
# <a name="debugging-a-service-application"></a>调试服务应用程序


*服务* 也称为 *windows 服务*，是一种用户模式进程，旨在由无人参与交互的 Windows 启动。 它在系统启动时自动启动，或者由使用 Win32 API 中包含的服务功能的应用程序启动。 用户还可以通过 "服务控制面板" 实用程序来启动服务。 每个服务都必须符合服务控制管理器 (SCM) 的接口规则。

每个服务由三个元素组成： *服务应用程序*、 *服务控制程序* 和服务控制管理器本身。 尽管服务应用程序有时 (错误地) 称为 "服务"，但实际上它是组成服务的三个组件中的一个。 服务应用程序可以包含几乎任何类型的用户模式代码。 服务控制程序控制服务应用程序的启动和停止时间。 服务控制管理器是 Windows 的一部分。

以下部分介绍了如何调试服务应用程序：

[选择最佳方法](choosing-the-best-method.md)

[准备调试服务应用程序](preparing-to-debug-the-service-application.md)

[自动调试服务应用程序](debugging-the-service-application-automatically.md)

[手动调试服务应用程序](debugging-the-service-application-manually.md)

有关服务、服务应用程序和服务控制管理器的概述，请参阅 *microsoft Windows 内部内容： Microsoft Windows Server 2003、WINDOWS XP 和 windows 2000* ，按 David，将 Russinovich (第四版，Microsoft 按，2005) 。

 

 





