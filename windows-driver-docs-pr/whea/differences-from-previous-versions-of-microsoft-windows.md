---
title: 与早期版本的 Microsoft Windows 的差异
description: 与早期版本的 Microsoft Windows 的差异
ms.assetid: 9c30c5c6-27a7-424e-b5f0-ab625eed4b8a
keywords:
- Windows 硬件错误体系结构 WDK，早期 Windows 版本
- WHEA WDK，与早期 Windows 版本的比较
- 硬件错误 WDK WHEA，早期 Windows 版本
- 错误 WDK WHEA，早期 Windows 版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ad3b9310580adb6a1c8d09ba3f7e7bb2c7d009b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354533"
---
# <a name="differences-from-previous-versions-of-microsoft-windows"></a>与早期版本的 Microsoft Windows 的差异


以下列表总结了 Windows 硬件错误体系结构 (WHEA) 和硬件中的错误处理的 Windows Vista 之前的 Microsoft Windows 版本之间的差异。

### <a name="error-handling-in-previous-versions-of-windows"></a>**以前版本的 Windows 中的错误处理**

-   包括大量不相关的错误报告机制

-   具有不同错误信号和报告机制为每个处理器体系结构

-   没有办法为操作系统以确定由特定的硬件平台支持哪些错误源

-   不会捕获所有可用的错误信息

-   不会有效地使用现有或未来的硬件错误标准

-   未能有效地利用任何特定于平台的功能，

-   提供了有关报告错误数据没有通用的错误记录格式

-   提供了致命硬件错误; 没有错误记录持久性机制重新启动系统时，会丢失明显的错误数据

-   提供了用于处理 I/O 硬件错误的不佳支持

-   提供了一些错误恢复的支持

-   为提供了一些支持错误管理应用程序

-   难以确定硬件错误的根本原因

-   提供处理实现的不够灵活的平台和固件供应商的硬件错误

### <a name="windows-hardware-error-architecture"></a>**Windows 硬件错误体系结构**

-   包括常见的错误报告基础结构的所有处理器体系结构和硬件平台上的所有硬件错误

-   包括用于确定特定的硬件平台支持的错误源的错误源发现机制\*

-   使操作系统来捕获所有可用的错误信息

-   充分地利用现有硬件错误标准的并允许通过使用新的平台特定硬件错误驱动程序 (PSHEDs) 支持未来的硬件错误标准

-   可以使用 PSHED 插件来充分利用特定于平台的功能

-   使用常用[错误记录](error-records.md)用于所有类型的硬件错误的格式

-   包括的错误记录持久性机制致命硬件错误而重新启动系统将保留完整的错误记录\*

-   提供用于处理 I/O 硬件错误的增强的支持

-   包括用于从非致命硬件错误中恢复的基础结构\*

-   错误管理应用程序可以通过基于 ETW 的错误事件报告和用户模式错误管理 API 提供支持\*

-   更轻松地确定硬件错误的根本原因

-   提供了新的平台和固件供应商的硬件错误实现的替代方案\*

**请注意**  项以星号标识 (\*) 支持 Windows Server 2008、 Windows Vista SP1 和更高版本的 Windows 中。

 

 

 




