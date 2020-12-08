---
title: UMDF 如何报告错误
description: 本主题介绍 User-Mode Driver Framework (UMDF) 报告错误的方式。 它适用于 UMDF 版本1和2。
keywords:
- User-Mode Driver Framework WDK，错误
- UMDF WDK，错误
- 用户模式驱动程序 WDK UMDF，错误
- 错误 WDK UMDF
- Windows 错误报告 WDK UMDF
- WER WDK UMDF
- 报告 WDK UMDF 错误
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dd76cdfd28292fae480b8a7478fd3ff36956ad0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815607"
---
# <a name="how-umdf-reports-errors"></a>UMDF 如何报告错误


本主题介绍 User-Mode Driver Framework (UMDF) 报告错误的方式。 它适用于 UMDF 版本1和2。

当 UMDF 驱动程序崩溃时，框架会创建一个 Windows 错误报告 (WER) 报表。

UMDF 报告以下类型的错误：

-   [UMDF 验证](using-umdf-verifier.md) 程序失败。

-   宿主进程中出现未经处理的异常。

-   宿主进程意外终止。

-   关键操作的故障或超时。 有关超时的详细信息，请参阅 [在 UMDF 中主机进程超时](how-umdf-enforces-time-outs.md)。

UMDF 错误报告可以包含以下信息。 报表的内容取决于检测到的问题。

-   主机进程的内存转储

-   UMDF 跟踪日志的副本

-   有关设备的配置信息，其中可能包括设备名称、制造商、已安装的驱动程序和驱动程序二进制文件版本

-   分析问题，其中可以包括上次从驱动程序到框架的调用的地址 (，反之亦然) ，问题代码，异常信息等

 

 





