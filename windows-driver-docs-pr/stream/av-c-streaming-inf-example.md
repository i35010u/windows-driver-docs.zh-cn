---
title: AV/C 流式处理 INF 示例
description: AV/C 流式处理 INF 示例
keywords:
- AV/C WDK，流筛选器驱动程序
- 流筛选器驱动程序 WDK AV/C
- Avcstrm.sys 流筛选器驱动程序 WDK、INF 示例
- INF 文件 WDK AV/C 流式处理
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5cdc40ba0dc49a2a57f94200ae995c2bdea57aa3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832061"
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
