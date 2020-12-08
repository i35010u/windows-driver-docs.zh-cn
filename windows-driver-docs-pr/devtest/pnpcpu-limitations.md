---
title: PNPCPU 限制
description: PNPCPU 限制
keywords:
- PNPCPU WDK，限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8441cab693c2bec5b32efc314135413812220aa0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841037"
---
# <a name="pnpcpu-limitations"></a>PNPCPU 限制


**注意**   不支持在受许可证限制的计算机上运行此工具。 如果系统使用的 Cpu 少于系统中实际存在的 Cpu，原因是已安装版本的许可限制，则不能使用 Pnpcpu 工具。

 

-   执行 **-add** 命令一次后，必须重新启动计算机。 不能执行热删除使用 **-add** 命令添加的处理器。

-   "任务管理器" 和 "系统设备管理器视图" 之间的差异在于 Windows (任务管理器视图) 所使用的处理器数量之间的差异，以及由 ACPI (设备管理器视图) 或测试的处理器枚举器驱动程序可以管理的数字。

-   加载自定义总线枚举器驱动程序时，将不会加载默认处理器驱动程序，因此设备管理器中显示的每个处理器上的错误代码为28。

-   执行热添加操作后，每个处理器设备管理器中都有两个条目，一个具有错误代码28，另一个不包含。 在 **View** &gt; 设备管理器中选择 "**按连接查看设备**" 时，会看到 " **Microsoft ACPI-Compliant 系统**" 下每个处理器的一个实例，并且每个处理器的第二个实例位于 "**处理器总线枚举器**" 下，后者将是实际正在运行的实例。

 

 





