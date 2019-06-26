---
title: AV/C 流式处理 INF 示例
description: AV/C 流式处理 INF 示例
ms.assetid: c8a2c9cd-c71b-4fd1-80f5-34d13837865e
keywords:
- AV/C WDK，Stream 筛选器驱动程序
- Stream 筛选器驱动程序 WDK AV/C
- Avcstrm.sys 流式处理筛选器驱动程序 WDK、 INF 示例
- INF 文件 WDK AV/C 流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6717b21fb421315c1418bc8383392e78c8c6f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386764"
---
# <a name="avc-streaming-inf-example"></a>AV/C 流式处理 INF 示例





（在子单元设备驱动程序安装） 的功能驱动程序的 INF 文件将安装*Avcstrm.sys*作为驱动程序堆栈上的较低的筛选器驱动程序。 INF 文件包含"。*hw*"部分来执行安装设备。 下面的代码示例演示如何添加*Avcstrm.sys*作为在 Windows 2000 或更高版本操作系统或 Windows Millennium Edition、 Windows 98 或 Windows 95 或更高版本的操作系统，使用较低的筛选器驱动程序"子单元"作为安装节名称：

```INF
[Subunit.HW]
AddReg=Subunit_AddFilter_W9x

[Subunit.NT.HW]
AddReg=Subunit_AddFilter_NT

[SubUnit_AddFilter_W9x]
HKR,,"LowerFilters",0x00010000,"avcstrm.sys"; Win9X use "avcstrm.sys" as driver name

[Subunit_AddFilter_NT]
HKR,,"LowerFilters",0x00010000,"AVCSTRM"; NT use this "AVCSTRM" as Service name
```

Windows 2000 和更高版本，功能驱动程序还必须进行必要的驱动程序依赖关系服务中安装部分，以保持合适的驱动程序加载顺序。 在以下示例中，AVCSTRM 服务部分加载之前的子单元驱动程序：

```INF
ServiceBinary = %12%\subunit.sys
Dependencies  = AVCSTRM   ; loaded before subunit.sys
```

有关设备安装文件的详细信息，请参阅[INF 文件的部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)。

 

 




