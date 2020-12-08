---
title: 识别源磁盘和文件
description: 识别源磁盘和文件
keywords:
- INF 文件 WDK 显示，标识源磁盘或文件
- 源磁盘 WDK 显示
- 源文件 WDK 显示
- 标识显示源磁盘或文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4bbfbe228d291e9a17044f2777b6f9c9b7f6510
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839597"
---
# <a name="identifying-source-disks-and-files"></a>识别源磁盘和文件


必须在 " **SourceDisksNames** " 和 " **SourceDisksFiles** " 部分中指定所有内置的显示驱动程序。 以下示例显示了如何识别 cd-rom 光盘以及磁盘上包含的源文件的名称。 在安装过程中，源文件将传输到目标计算机。

```inf
[SourceDisksNames]
3426=windows cd

[SourceDisksFiles]
DisplayMiniportDriverName.sys  = 3426
UserModeDriverName1.dll  = 3426
UserModeDriverName2.dll  = 3426
```

有关 **SourceDisksNames** 和 **SourceDisksFiles** 部分的详细信息，请参阅 [**Inf SourceDisksNames 部分**](../install/inf-sourcedisksnames-section.md) 和 [**inf SourceDisksFiles 部分**](../install/inf-sourcedisksfiles-section.md)。

 

