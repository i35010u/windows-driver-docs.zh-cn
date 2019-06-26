---
title: 识别源磁盘和文件
description: 识别源磁盘和文件
ms.assetid: 0eb8fe7f-1e44-4f3d-8567-31a2cd659805
keywords:
- INF 文件 WDK 显示标识源磁盘或文件
- 源磁盘 WDK 显示
- 源代码文件 WDK 显示
- 确定显示源磁盘或文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6815050947045be29ca067fc90f20949bd047e7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380177"
---
# <a name="identifying-source-disks-and-files"></a>识别源磁盘和文件


必须指定所有的框中显示驱动程序中**SourceDisksNames**并**SourceDisksFiles**部分。 下面的示例演示如何识别 CD-ROM 光盘和在磁盘包含的源文件的名称。 在源代码文件传输到目标计算机在安装过程。

```inf
[SourceDisksNames]
3426=windows cd

[SourceDisksFiles]
DisplayMiniportDriverName.sys  = 3426
UserModeDriverName1.dll  = 3426
UserModeDriverName2.dll  = 3426
```

有关详细信息**SourceDisksNames**并**SourceDisksFiles**部分中，请参阅[ **INF SourceDisksNames 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksnames-section)和[ **INF SourceDisksFiles 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-sourcedisksfiles-section)。

 

 





