---
title: 与早期版本的 Microsoft Windows 的差异
description: 与早期版本的 Microsoft Windows 的差异
keywords:
- Windows 硬件错误体系结构 WDK，早期 Windows 版本
- WHEA WDK，与早期 Windows 版本的比较
- 硬件错误 WDK WHEA，早期 Windows 版本
- 错误 WDK WHEA，早期 Windows 版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e92939d89285b1524cd1801cfc2f16c1061e1fd6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822687"
---
# <a name="differences-from-previous-versions-of-microsoft-windows"></a>与早期版本的 Microsoft Windows 的差异


以下列表汇总了 windows Vista 之前的 Microsoft Windows 版本中的 Windows 硬件错误体系结构 (WHEA) 与硬件错误处理之间的差异。

### <a name="error-handling-in-previous-versions-of-windows"></a>**以前版本的 Windows 中的错误处理**

-   包括许多无关的错误报告机制

-   为每个处理器体系结构提供不同的错误信号和报告机制

-   对于操作系统，不能确定特定硬件平台支持的错误源

-   不捕获所有可用错误信息

-   不会有效地使用现有或未来的硬件错误标准

-   不能有效地利用任何特定于平台的功能

-   不提供报告错误数据的常见错误记录格式

-   为致命硬件错误提供无错误记录永久性机制;当系统重新启动时，会丢失大量错误数据

-   提供对处理 i/o 硬件错误的不太支持

-   为错误恢复提供少量支持

-   只提供对错误管理应用程序的支持

-   难以确定硬件错误的根本原因

-   为平台和固件供应商的硬件错误处理实现提供了极大的灵活性

### <a name="windows-hardware-error-architecture"></a>**Windows 硬件错误体系结构**

-   包含所有处理器体系结构和硬件平台上的所有硬件错误的常见错误报告基础结构

-   包含错误源发现机制，用于确定特定硬件平台支持的错误源\*

-   使操作系统能够捕获所有可用错误信息

-   充分利用现有硬件错误标准，并通过使用新的特定于平台的硬件错误驱动程序 (PSHEDs) ，为将来的硬件错误标准提供支持

-   允许你使用 PSHED 插件来利用特定于平台的功能

-   对于所有类型的硬件错误，使用常见 [错误记录](error-records.md) 格式

-   包含错误记录在系统重新启动时保留完整错误记录的严重硬件错误的持久性机制\*

-   提供对处理 i/o 硬件错误的增强支持

-   包括用于从非严重硬件错误中恢复的基础结构\*

-   通过基于 ETW 的错误事件报告和用户模式错误管理 API，提供对错误管理应用程序的支持\*

-   更易于确定硬件错误的根本原因

-   为平台和固件供应商的硬件错误实现提供了新的替代方案\*

**注意**  \* Windows Server 2008、Windows VISTA SP1 和更高版本的 windows 支持用星号 () 标识的项。

 

 

 




