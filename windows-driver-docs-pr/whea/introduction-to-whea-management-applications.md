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
ms.openlocfilehash: 83059d3bd9ef0b279fb85fb4d966c1f0f6926560
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843134"
---
# <a name="introduction-to-whea-management-applications"></a>WHEA 管理应用程序简介


Windows 硬件错误体系结构（WHEA）提供了一个 Windows Management Instrumentation （WMI）接口，该接口允许用户模式应用程序执行 WHEA 管理操作。 WHEA 管理界面由以下 WMI 提供程序类组成：

<a href="" id="wheaerrorsourcemethods"></a>[WHEAErrorSourceMethods](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)  
此类实现用于管理系统中的[错误源](hardware-errors-and-error-sources.md)的方法。

<a href="" id="wheaerrorinjectionmethods"></a>[WHEAErrorInjectionMethods](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)  
此类实现将硬件错误注入硬件平台的方法。

用户模式应用程序通过调用**IWbemServices：： ExecMethod**方法间接调用这些类中的方法。 有关如何调用 WMI 提供程序类中的方法的详细信息，请参阅 Microsoft Windows SDK 文档中的 "[调用提供程序方法](https://go.microsoft.com/fwlink/p/?linkid=80945)" 主题。

有关 WMI 的详细信息，请参阅 Windows SDK 文档的[Windows Management Instrumentation](https://go.microsoft.com/fwlink/p/?linkid=80947)部分。

**请注意**  在 windows Server 2008、WINDOWS Vista SP1 和更高版本的 windows 中支持 WHEA WMI 提供程序类。

 

 

 




