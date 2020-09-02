---
title: PoolMon
description: PoolMon
ms.assetid: 3cda6297-0e6f-48d5-b9d9-670ccf102c86
keywords:
- PoolMon WDK
- 池监视器 WDK
- 池标记 WDK PoolMon
- 内存池监视器 WDK
- 驱动程序测试 WDK，PoolMon
- 测试驱动程序 WDK，PoolMon
- 分配池标记 WDK PoolMon
- 内存分配 WDK PoolMon
- 显示内存分配数据
- 内存 WDK PoolMon
- 终端服务会话 WDK PoolMon
- 标记文件 WDK PoolMon
- 统计信息 WDK PoolMon
- 状态信息 WDK PoolMon
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f461497675b7e492d768b6209d786ef555c20428
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382403"
---
# <a name="poolmon"></a>PoolMon


## <span id="ddk_poolmon_tools"></span><span id="DDK_POOLMON_TOOLS"></span>


PoolMon ( # A0) ，内存池监视器显示操作系统从系统分页和非分页内核池收集的内存分配数据，以及用于终端服务会话的内存池。 数据按池分配标记进行分组。

当驱动程序开发人员和测试人员创建新的驱动程序、更改驱动程序代码或对驱动程序进行压力时，通常使用 PoolMon 来检测内存泄漏。 你还可以在测试的每个阶段使用 PoolMon 来查看驱动程序的分配模式和自由操作模式，并显示驱动程序在任何给定时间使用的池内存量。

本文档中所述的 PoolMon 版本包含在 \\ \\ [Windows 驱动程序工具包 (WDK) ](../download-the-wdk.md)的工具的其他子目录中。

本主题包括以下内容：

[PoolMon 概述](poolmon-overview.md)

[PoolMon 要求](poolmon-requirements.md)

[PoolMon 命令](poolmon-commands.md)

[PoolMon 显示](poolmon-display.md)

[PoolMon 示例](poolmon-examples.md)

若要在 Microsoft Windows XP 和更早的系统上使用 PoolMon，必须启用 *池标记*。 在 Windows Server 2003 和更高版本的 Windows 上，将永久启用池标记。 有关详细信息，请参阅 [PoolMon 要求](poolmon-requirements.md)中的 "池标记要求"。

PoolMon 可以显示 Windows 组件的名称，以及分配每个池标记的常用驱动程序的名称。 此功能使用 pooltag.txt 中的数据、使用 PoolMon 安装的文件以及用于 Windows 包的调试工具。

