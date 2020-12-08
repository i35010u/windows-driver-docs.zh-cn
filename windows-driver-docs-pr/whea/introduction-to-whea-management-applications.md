---
title: WHEA 管理应用程序简介
description: WHEA 管理应用程序简介
keywords:
- 管理应用程序 WDK WHEA，关于管理应用程序
- 用户模式应用程序 WDK WHEA，管理应用程序
- WHEA WDK，管理应用程序
- Windows 硬件错误体系结构 WDK，管理应用程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9b85a9fc09a5be77670642c90d3531cff931e71
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787113"
---
# <a name="introduction-to-whea-management-applications"></a>WHEA 管理应用程序简介


Windows 硬件错误体系结构 (WHEA) 提供 Windows Management Instrumentation (WMI) 接口，该接口允许用户模式应用程序执行 WHEA 管理操作。 WHEA 管理界面由以下 WMI 提供程序类组成：

<a href="" id="wheaerrorsourcemethods"></a>[WHEAErrorSourceMethods](/windows-hardware/drivers/ddi/_whea/)  
此类实现用于管理系统中的 [错误源](hardware-errors-and-error-sources.md) 的方法。

<a href="" id="wheaerrorinjectionmethods"></a>[WHEAErrorInjectionMethods](/windows-hardware/drivers/ddi/_whea/)  
此类实现将硬件错误注入硬件平台的方法。

用户模式应用程序通过调用 **IWbemServices：： ExecMethod** 方法间接调用这些类中的方法。 有关如何调用 WMI 提供程序类中的方法的详细信息，请参阅 Microsoft Windows SDK 文档中的 " [调用提供程序方法](/windows/win32/wmisdk/calling-a-provider-method) " 主题。

有关 WMI 的详细信息，请参阅 Windows SDK 文档的 [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page) 部分。

**注意**  Windows Server 2008、Windows Vista SP1 和更高版本的 Windows 支持 WHEA WMI 提供程序类。

 

