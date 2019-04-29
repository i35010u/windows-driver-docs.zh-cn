---
title: 调试服务应用程序
description: 调试服务应用程序
ms.assetid: 1d1e24d5-8b6b-4ed5-84ad-b73356168b10
keywords:
- 服务应用程序调试
- 总结调试、 调试服务应用程序
- 服务
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c40ac56795bcc2d316cbed96c3ea289eac23122
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324641"
---
# <a name="debugging-a-service-application"></a>调试服务应用程序


一个*服务*，也称为*Windows 服务*，是旨在通过 Windows 而无需人工交互来启动用户模式进程。 在系统启动，或使用 Win32 API 中包含的服务功能的应用程序，它是自动启动。 也可以通过服务控制面板实用程序通过用户启动一项服务。 每个服务必须符合服务控制管理器 (SCM) 的接口规则。

每个服务由三个元素组成：*服务应用程序*即*服务控制程序*，和服务控制管理器本身。 尽管有时是服务应用程序 （错误地） 称为"服务"，实际上它是构成服务的三个组件之一。 服务应用程序可以包含几乎任何类型的用户模式代码。 服务控制程序控制的服务应用程序启动和停止时。 服务控制管理器是 Windows 的一部分。

以下部分介绍如何调试服务应用程序：

[选择最佳方法](choosing-the-best-method.md)

[调试服务应用程序的准备工作](preparing-to-debug-the-service-application.md)

[自动调试服务应用程序](debugging-the-service-application-automatically.md)

[手动调试服务应用程序](debugging-the-service-application-manually.md)

有关服务、 服务应用程序和服务控制管理器的概述，请参阅*Microsoft Windows 内部结构：Microsoft Windows Server 2003、 Windows XP 和 Windows 2000*由 David A.Solomon 和 Mark E.Russinovich （第四个版本，Microsoft Press，2005年）。

 

 





