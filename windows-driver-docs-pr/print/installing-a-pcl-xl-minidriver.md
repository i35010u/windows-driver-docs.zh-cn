---
title: 安装 PCL XL 微型驱动程序
description: 安装 PCL XL 微型驱动程序
ms.assetid: 88e4e1a0-8adb-4f40-abeb-a4da761ca4ee
keywords:
- PCL XL 矢量图形 WDK Unidrv，安装微型驱动程序
- 微型驱动程序 WDK PCL XL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36202095f6d007dc86d2177a8dc6e7c43cd226b2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362307"
---
# <a name="installing-a-pcl-xl-minidriver"></a>安装 PCL XL 微型驱动程序





Ntprint.inf 中 Windows XP 及更高版本，具有以下\[PCLXL。OEM\]部分：

```cpp
[PCLXL.OEM]
CopyFiles=PCLXL,@PCL5ERES.DLL
```

[ **INF CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)将所有中列出的文件复制\[PCLXL\]部分中，以及 pcl5eres.dll 的默认目标目录。 \[PCLXL\]部分也将出现在 ntprint.inf 并列出了要复制的文件。

```cpp
[PCLXL]
PCLXL.DLL
PCLXL.GPD
P6FONT.GPD
PJL.GPD
P6DISP.GPD
```

Pclxl.dll 包含 PCL XL *UFMs*和各种资源字符串。 本部分中列出的其他 GPDs 是 PCL XL (PCL 6) 的支持文件。

若要安装 PCL XL 打印机微型驱动程序，OEM 应添加特定于打印机的 INF 部分如下所示。 Ntprint.inf 之前，将加载此 INF。

```cpp
[P6SAMPLE.GPD]
CopyFiles=@P6SAMPLE.GPD
DataSection=UNIDRV_DATA
DataFile=P6SAMPLE.GPD
Include=NTPRINT.INF
Needs=UNIDRV.OEM,TTFSUB.OEM,PCLXL.OEM
```

在前面部分中， **CopyFiles** OEM 的 GPD 文件 (在此示例中名为 p6sample.gpd) 复制的第一行中的指令。 与关联的条目**DataSection**指令的第二行中 (请参阅[打印机 INF 文件的数据部分](printer-inf-file-data-sections.md)并[打印机 INF 文件安装的部分](printer-inf-file-install-sections.md)) 是指\[UNIDRV\_数据\]ntprint.inf 中的部分。 **DataFile**第三行中的指令指定了该 p6sample.gpd 是与此打印机微型驱动程序相关联的数据文件。 第四行将会导致 ntprint.inf 要包含。 中的三个条目**需要**指令的第五个行，请参阅在 ntprint.inf 中的名称同为部分。 这样，要获取其 driver.cab 中加载的文件的访问权限的 INF 文件。

有关使用的其他信息**CopyFiles**指令对于打印机安装，请参阅[打印机 INF 文件 CopyFiles 部分](printer-inf-file-copyfiles-sections.md)。

 

 




