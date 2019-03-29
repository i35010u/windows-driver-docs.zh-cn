---
title: 跟踪工具在哪里？
description: 跟踪工具在哪里？
ms.assetid: fceb5c8b-bc0a-4708-b925-e6fb76328f7e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35886d4ca4818cbdd151468574da187efe09308c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577524"
---
# <a name="where-are-the-tracing-tools"></a>跟踪工具位于何处？


在 Windows 驱动程序工具包 (WDK) 8.1，许多跟踪工具，如[Tracefmt](tracefmt.md)并[Tracelog](tracelog.md)，位于 %windowssdkdir%\\bin\\*平台*目录。 其中，%windowssdkdir%是安装了 WDK 和 SDK，其中的目录和*平台*是 x64 或 x86。 其他的跟踪工具，例如 Logman.exe，是 Windows 操作系统附带的。

[TraceView](traceview.md)位于 %windowssdkdir%\\工具\\*平台*目录。

跟踪工具及其位置的完整列表，请参阅[软件跟踪工具的调查](survey-of-software-tracing-tools.md)并[索引的 Windows 驱动程序工具包工具](index-of-windows-driver-kit-tools.md)。

 

 





