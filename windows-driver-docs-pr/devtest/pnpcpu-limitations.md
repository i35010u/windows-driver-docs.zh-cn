---
title: PNPCPU 限制
description: PNPCPU 限制
ms.assetid: e25a54e7-cf6f-4723-9bf3-3b68cce8ec7e
keywords:
- PNPCPU WDK 限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59049fbd497a3cd7f8ac040ec44ce5e1bffb36cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352443"
---
# <a name="pnpcpu-limitations"></a>PNPCPU 限制


**请注意**  在计算机上运行此工具是由许可证限制是不受支持。 如果系统正在使用较少的 Cpu 比以物理方式中会出现由于许可限制系统已安装的版本，则无法使用 Pnpcpu 工具。

 

-   已执行后 **-添加**命令后，必须重新启动计算机。 不能执行的处理器使用添加热删除 **-添加**命令。

-   从 Windows （任务管理器视图） 正在使用的处理器数和处理器驱动程序可以管理数量之间的区别系统结果任务管理器和设备管理器视图之间的差异被枚举ACPI （设备管理器视图） 或测试的处理器的枚举器驱动程序。

-   加载自定义总线枚举器驱动程序时，默认处理器驱动程序将不加载，因此在设备管理器中显示每个处理器上的错误代码 28。

-   执行后热添加操作，则会为每个处理器的两个条目设备管理器中，一个具有错误代码 28 和其他非。 当选择**视图** &gt; **依连接排序设备**在设备管理器中，您将看到在每个处理器的一个实例**Microsoft 符合 ACPI 系统**，并为每个下的第二个实例**处理器总线枚举器**，它将是实际正在运行的实例。

 

 





