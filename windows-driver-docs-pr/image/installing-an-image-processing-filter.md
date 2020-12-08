---
title: 安装图像处理筛选器
description: 安装图像处理筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dcec1b4d692c410423414953c3ee8fd20bad93d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839249"
---
# <a name="installing-an-image-processing-filter"></a>安装图像处理筛选器





图像处理筛选器通常与 WIA 驱动程序一起安装。 若要将驱动程序的图像处理筛选器与驱动程序一起安装，必须为驱动程序的 INF 文件添加少量的添加操作。 下面的示例演示了如何修改现有驱动程序 INF 文件以包含图像处理筛选器的示例。

```INF
[MyDriver.AddReg]
...
HKCR,CLSID\<UiClassId>\shellex\ImageProcessingFilter\<FilterClassId>
...
HKCR,CLSID\<FilterClassId>,,,"My Image Processing Filter"
HKCR,CLSID\<FilterClassId>\InProcServer32,,,%11%\Myimgfilter.dll
HKCR,CLSID\<FilterClassId>\InProcServer32,ThreadingModel,,"Apartment"
...

[MyDriver.CopyFiles]
...
Myimgfilter.dll
...

[SourceDisksFiles.x86]
...
Myimgfilter.dll=1
...
```

*&lt; UiClassId &gt;* 值是驱动程序为 WIA \_ DIP UI CLSID 属性返回的类 id \_ \_ ，而 *&lt; FILTERCLASSID &gt;* 是图像处理筛选器实现的类 id。 在此示例中， *Myimgfilter.dll* 包含图像处理筛选器的实现。

**AddReg** 节中的第一项是将图像处理筛选器注册为驱动程序的扩展，并使用以下三个项将图像处理筛选器注册为 COM 组件。

如前面的示例 INF 代码段中所示，图像处理筛选器的 INF 文件中建议的 **ThreadingModel** 值为 **单元**。

**注意**   驱动程序安装完成后，可以安装筛选器（例如，作为增值组件）。

 

 

 




