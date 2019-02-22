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
- WDK PoolMon 的统计信息
- WDK PoolMon 的状态信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36966ba65ca5d337e9af9808d990e8fb4ec93a39
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520441"
---
# <a name="poolmon"></a>PoolMon


## <span id="ddk_poolmon_tools"></span><span id="DDK_POOLMON_TOOLS"></span>


PoolMon (poolmon.exe) 内存池监视器，显示的操作系统从分页系统收集有关内存分配数据和非分页的内核池和用于终端服务会话使用的内存池。 按池分配标记分组数据。

驱动程序开发人员和测试人员通常使用 PoolMon 检测内存泄漏时不创建新的驱动程序、 更改驱动程序代码中，或强调该驱动程序。 此外可以使用 PoolMon 测试的每个阶段中可查看分配和 free 操作的驱动程序的模式，并以显示该驱动程序使用在任何给定时间的池内存量。

本文档中所述的 PoolMon 版本包含在\\工具\\的其他子目录[Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=846744)。

本主题包括以下内容：

[PoolMon 概述](poolmon-overview.md)

[PoolMon 要求](poolmon-requirements.md)

[PoolMon 命令](poolmon-commands.md)

[PoolMon 显示](poolmon-display.md)

[PoolMon 示例](poolmon-examples.md)

若要在 Microsoft Windows XP 和早期系统上使用 PoolMon，必须启用*池标记*。 在 Windows Server 2003 和更高版本的 Windows，永久启用池标记。 详细信息，请参阅"池标记要求"中[PoolMon 要求](poolmon-requirements.md)。

PoolMon 可以显示 Windows 组件的名称，常用于分配每个池标记的驱动程序。 此功能使用 pooltag.txt，安装与 PoolMon，并为 Windows 调试工具软件包的文件中的数据。 有时，Microsoft 将会更新此文件。 若要检查更新，请转到[Microsoft 支持部门](https://go.microsoft.com/fwlink/p/?linkid=8713)网站，搜索"pooltag.txt。"

 

 





