---
title: 识别源磁盘和文件
description: 识别源磁盘和文件
ms.assetid: 0eb8fe7f-1e44-4f3d-8567-31a2cd659805
keywords:
- INF 文件 WDK 显示，标识源磁盘或文件
- 源磁盘 WDK 显示
- 源文件 WDK 显示
- 标识显示源磁盘或文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81cd5a1fa5ab959a68bb8a2502dde3cdf1c18bb5
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064096"
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

 

