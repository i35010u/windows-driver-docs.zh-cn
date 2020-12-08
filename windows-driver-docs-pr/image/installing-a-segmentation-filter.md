---
title: 安装分段筛选器
description: 安装分段筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0393a4a9edacbfc8e70a9ed9aa33dae28a814022
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793639"
---
# <a name="installing-a-segmentation-filter"></a>安装分段筛选器





分段筛选器应与 WIA 驱动程序一起安装。 为此，必须对驱动程序的 INF 文件进行少量的添加。 以下 INF 示例显示了如何修改现有的驱动程序 INF 文件以包含分段筛选器。

```INF
[MyDriver.AddReg]
...
HKCR,CLSID\<UiClassId>\shellex\SegmentationFilter\<FilterClassId>
...
HKCR,CLSID\<FilterClassId>,,,"My Segmentation Filter"
HKCR,CLSID\<FilterClassId>\InProcServer32,,,%11%\Mysegfilter.dll
HKCR,CLSID\<FilterClassId>\InProcServer32,ThreadingModel,,"Both"
...
 
[MyDriver.CopyFiles]
...
Mysegfilter.dll
...
 
[SourceDisksFiles.x86]
...
Mysegfilter.dll=1
...
```

*&lt; UiClassId &gt;* 是驱动程序为 WIA \_ DIP \_ UI CLSID 属性返回的值 \_ 。 *&lt; FilterClassId &gt;* 是分段筛选器实现的类 ID。 *Mysegfilter.dll* 是包含分段筛选器的实现的 DLL。

设备 [**INF AddReg 指令**](../install/inf-addreg-directive.md) 中的第一个条目将分段筛选器注册为驱动程序的扩展，接下来的三个条目将分段筛选器注册为 COM 组件。

如果驱动程序使用 Microsoft 提供的 WIA 分段筛选器，则不需要设备的 [**INF CopyFiles 指令**](../install/inf-copyfiles-directive.md)、 [**INF SourceDisksFiles 部分**](../install/inf-sourcedisksfiles-section.md)和最后三个注册表项。 唯一的要求是微型驱动程序实现 WIA \_ IPS \_ 分段属性。

COM **ThreadingModel** 必须同时为 **两者**。

有关 INF 文件的详细信息，请参阅 [WIA 设备的 INF 文件](inf-files-for-wia-devices.md)。

 

