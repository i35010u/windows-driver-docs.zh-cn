---
title: AV/C 流式处理 INF 示例
description: AV/C 流式处理 INF 示例
ms.assetid: c8a2c9cd-c71b-4fd1-80f5-34d13837865e
keywords:
- AV/C WDK，流筛选器驱动程序
- 流筛选器驱动程序 WDK AV/C
- Avcstrm.sys 流筛选器驱动程序 WDK、INF 示例
- INF 文件 WDK AV/C 流式处理
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2eab13c5002098ccfd9262e2886275126126c172
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186833"
---
# <a name="avc-streaming-inf-example"></a>AV/C 流式处理 INF 示例

在子单位设备驱动程序安装过程中 (函数驱动程序的 INF 文件) 将 *Avcstrm.sys* 安装为驱动程序堆栈上的较低筛选器驱动程序。 INF 文件包含 ""。*hw*"部分。 下面的代码示例演示如何使用 "子区域" 作为安装部分名称，将 *Avcstrm.sys* 添加为较低筛选器驱动程序：

```inf
[Subunit.NT.HW]
AddReg=Subunit_AddFilter_NT

[Subunit_AddFilter_NT]
HKR,,"LowerFilters",0x00010000,"AVCSTRM"; NT use this "AVCSTRM" as Service name
```

函数驱动程序还必须在服务安装部分中进行必要的驱动程序依赖关系，以保留正确的驱动程序加载顺序。 

在下面的示例中，AVCSTRM service 节加载到了子单元驱动程序之前：

```inf
ServiceBinary = %12%\subunit.sys
Dependencies  = AVCSTRM   ; loaded before subunit.sys
```

有关设备安装文件的详细信息，请参阅 [Inf 文件部分](../install/inf-classinstall32-section.md) 和 [inf 文件指令](../install/inf-addcomponent-directive.md)。