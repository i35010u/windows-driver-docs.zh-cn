---
title: UMDF 如何报告错误
description: 本主题介绍如何将用户模式驱动程序框架 (UMDF) 报告错误。 它适用于这两种 UMDF 版本 1 和 2。
ms.assetid: 44e4e5df-d968-4973-8a36-e93c75320ff6
keywords:
- 用户模式驱动程序框架 WDK 错误
- UMDF WDK 错误
- 用户模式驱动程序 WDK UMDF，错误
- 错误 WDK UMDF
- Windows 错误报告 WDK UMDF
- WER WDK UMDF
- 错误报告 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ca2c3fd39ea7ebe57309f5bfc3721b7acb02b77
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390186"
---
# <a name="how-umdf-reports-errors"></a>UMDF 如何报告错误


本主题介绍如何将用户模式驱动程序框架 (UMDF) 报告错误。 它适用于这两种 UMDF 版本 1 和 2。

当 UMDF 驱动程序崩溃时，框架将创建一个 Windows 错误报告 (WER) 报表。

UMDF 报告以下类型的错误：

-   [UMDF Verifier](using-umdf-verifier.md)失败。

-   在主机进程的未处理的异常。

-   主机进程意外的终止。

-   失败或超时的关键操作。 有关超时的详细信息，请参阅[UMDF 中的主机进程超时](how-umdf-enforces-time-outs.md)。

UMDF 错误报表可以包含以下信息。 报表的内容取决于检测到的问题。

-   主机进程的内存转储

-   UMDF 跟踪日志的副本

-   有关设备，可以包括设备名称、 制造商、 驱动程序安装、 配置信息和驱动程序二进制文件版本

-   分析的问题，可以包含地址的最后一次的驱动程序框架调用 （反之亦然）、 问题代码、 异常信息等

 

 





