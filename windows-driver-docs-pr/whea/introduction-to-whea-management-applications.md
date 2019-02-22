---
title: WHEA 管理应用程序简介
description: WHEA 管理应用程序简介
ms.assetid: d0c487bd-dfa8-43f2-a494-0ed95d767bfb
keywords:
- 有关管理应用程序管理应用程序 WDK WHEA
- 用户模式应用程序 WDK WHEA，管理应用程序
- WHEA WDK，管理应用程序
- Windows 硬件错误体系结构 WDK，管理应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c36e0b701118b92d54d526575d9053f73263a600
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520633"
---
# <a name="introduction-to-whea-management-applications"></a>WHEA 管理应用程序简介


Windows 硬件错误体系结构 (WHEA) 提供了 Windows Management Instrumentation (WMI) 界面，允许用户模式应用程序执行 WHEA 管理操作。 WHEA 管理接口组成以下 WMI 提供程序类：

<a href="" id="wheaerrorsourcemethods"></a>[WHEAErrorSourceMethods](https://msdn.microsoft.com/library/windows/hardware/ff559521)  
此类实现用于管理方法[错误源](hardware-errors-and-error-sources.md)系统中。

<a href="" id="wheaerrorinjectionmethods"></a>[WHEAErrorInjectionMethods](https://msdn.microsoft.com/library/windows/hardware/ff559513)  
此类实现用于将硬件错误注入到的硬件平台的方法。

在用户模式应用程序调用的方法在这些类间接通过调用**iwbemservices:: Execmethod**方法。 有关如何在 WMI 提供程序类中调用方法的详细信息，请参阅[调用提供程序方法](https://go.microsoft.com/fwlink/p/?linkid=80945)Microsoft Windows SDK 文档中的主题。

有关 WMI 的详细信息，请参阅[Windows Management Instrumentation](https://go.microsoft.com/fwlink/p/?linkid=80947) Windows SDK 文档的部分。

**请注意**  WHEA WMI 提供程序类支持在 Windows Server 2008、 Windows Vista SP1 和更高版本的 Windows。

 

 

 




