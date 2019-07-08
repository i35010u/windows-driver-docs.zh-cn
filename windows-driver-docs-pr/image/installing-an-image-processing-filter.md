---
title: 安装图像处理筛选器
description: 安装图像处理筛选器
ms.assetid: bce6405f-0377-4e50-b898-28c6cdb962be
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f33e27ca3c5341326922589674415fe017145b02
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360035"
---
# <a name="installing-an-image-processing-filter"></a>安装图像处理筛选器





图像处理筛选器通常与 WIA 驱动程序一起安装。 若要安装该驱动程序以及驱动程序的图像处理筛选器，必须对驱动程序的 INF 文件完成少量的新增功能。 下面的示例演示如何修改现有的驱动程序 INF 文件以包括图像处理筛选器的示例。

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

*&lt;UiClassId&gt;* 值是类 ID，以驱动程序返回的 WIA\_DIP\_UI\_CLSID 属性，并且 *&lt;FilterClassId&gt;* 是图像处理筛选器实现的类 ID。 在此示例中， *Myimgfilter.dll*包含图像处理筛选器的实现。

中的第一个条目**AddReg**部分是作为扩展的驱动程序，注册图像处理筛选器和以下三项注册为 COM 组件的图像处理筛选器。

如前面的示例 INF 代码片段所示，推荐**ThreadingModel**图像处理筛选器的 INF 文件中的值是**单元**。

**请注意**  就可以安装一个筛选器后的驱动程序安装已完成--例如，作为增值的组件。

 

 

 




