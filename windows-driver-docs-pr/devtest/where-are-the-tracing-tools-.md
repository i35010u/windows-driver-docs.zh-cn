---
title: 跟踪工具在哪里
description: 跟踪工具在哪里
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f1cacf10f8179dd9d2ba2777dde6728b2ec4636
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810673"
---
# <a name="where-are-the-tracing-tools"></a>跟踪工具位于何处？


在 Windows 驱动程序工具包中 (WDK) 8.1，许多跟踪工具（例如 [Tracefmt](tracefmt.md)和 [Tracelog](tracelog.md)）都位于% WindowsSdkDir% \\ bin \\ *平台* 目录中。 其中，% WindowsSdkDir% 是安装了 WDK 和 SDK 的目录， *平台* 为 x64 或 x86。 其他跟踪工具（如 Logman.exe）都包含在 Windows 操作系统中。

[TraceView](traceview.md)位于% WindowsSdkDir% \\ 工具 \\ *平台* 目录中。

有关跟踪工具及其位置的完整列表，请参阅 [软件跟踪工具的调查](survey-of-software-tracing-tools.md) 和 [Windows 驱动程序工具包工具的索引](index-of-windows-driver-kit-tools.md)。

 

 





