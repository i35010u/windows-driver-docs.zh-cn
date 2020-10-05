---
title: WHEA 管理应用程序简介
description: WHEA 管理应用程序简介
ms.assetid: d0c487bd-dfa8-43f2-a494-0ed95d767bfb
keywords:
- 管理应用程序 WDK WHEA，关于管理应用程序
- 用户模式应用程序 WDK WHEA，管理应用程序
- WHEA WDK，管理应用程序
- Windows 硬件错误体系结构 WDK，管理应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982e70f9440b81bfc501ee6c0824c0d0bb4c838e
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91732656"
---
# <a name="introduction-to-whea-management-applications"></a>WHEA 管理应用程序简介


Windows 硬件错误体系结构 (WHEA) 提供 Windows Management Instrumentation (WMI) 接口，该接口允许用户模式应用程序执行 WHEA 管理操作。 WHEA 管理界面由以下 WMI 提供程序类组成：

<a href="" id="wheaerrorsourcemethods"></a>[WHEAErrorSourceMethods](/windows-hardware/drivers/ddi/_whea/)  
此类实现用于管理系统中的 [错误源](hardware-errors-and-error-sources.md) 的方法。

<a href="" id="wheaerrorinjectionmethods"></a>[WHEAErrorInjectionMethods](/windows-hardware/drivers/ddi/_whea/)  
此类实现将硬件错误注入硬件平台的方法。

用户模式应用程序通过调用 **IWbemServices：： ExecMethod** 方法间接调用这些类中的方法。 有关如何调用 WMI 提供程序类中的方法的详细信息，请参阅 Microsoft Windows SDK 文档中的 " [调用提供程序方法](/windows/win32/wmisdk/calling-a-provider-method) " 主题。

有关 WMI 的详细信息，请参阅 Windows SDK 文档的 [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page) 部分。

**注意**   Windows Server 2008、Windows Vista SP1 和更高版本的 Windows 支持 WHEA WMI 提供程序类。

 

