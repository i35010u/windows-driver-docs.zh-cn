---
title: V4 打印类驱动程序渲染
description: 为了进行呈现，v4 打印机驱动程序可以利用打印类驱动程序的现有呈现功能。
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: f0ff6b55204a3a8d97c4b571fe5573d41ceff842
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807489"
---
# <a name="v4-print-class-driver-rendering"></a>V4 打印类驱动程序渲染


为了进行呈现，v4 打印机驱动程序可以利用打印类驱动程序的现有呈现功能。

为了利用打印类驱动程序的现有呈现功能，v4 打印机驱动程序可以使用 **RequiredClass** v4 清单指令。 使用 **RequiredClass** 指令将导致驱动程序包含指定类驱动程序中的所有文件，并使用设备的驱动程序/友好名称及其 GUID 作为密钥。 这是用于将打印类驱动程序链接到特定于模型的打印机驱动程序的机制。

例如，名为 Fabrikam 并且打印类驱动程序名为 *PCL5e* 的公司可以使用以下示例打印驱动程序清单将其打印类驱动程序链接到其打印机驱动程序：

```Text
[DriverConfig]
DataFile=FAPDL.gpd
RequiredFiles=UNIRES.DLL,STDNAMES.GPD,STDDTYPE.GDL,STDSCHEM.GDL,STDSCHMX.GDL,MSXPSINC.GPD
RequiredClass="Fabrikam PCL5e Class Driver",{9343720D-B67E-4451-B93F-6F721C439771} ; This links the print class driver to this printer driver
ResourceFile=FARC.dll
PropertyBag=FAProperty.dpb
PrinterDriverID={GUID}
DriverCategory=PrintFax.Printer
ConstraintScript=faconst.js
EventFile=faevents.xml
PrinterExtensionUrl="https://www.fabrikam.com/download.asp?uiapp=120"

[BidiFiles]
BidiSPMFile=FABidiSPM.xml
BidiWSDFile=FABidiWSD.xml
BidiUSBFile=FaBidiUSB.xml
BidiUSBJSFile=FABidiUSBJS.js 

[DriverRender]
PageOutputQuality.Draft=MxdcImageType.JPEGHigh
PageOutputQuality.Normal= MxdcImageType.JPEGMedium
PageOutputQuality.High=MxdcImageType.PNG

[PrinterExtensions]
DriverEvent=FAapp.exe,{GUID}
PrintPreferences=FAapp.exe,{GUID2}
```

> [!NOTE]
> 类驱动程序无法使用 **RequiredClass** 指令。 当使用 **RequiredClass** 时，应避免在要链接到的打印机驱动程序和打印类驱动程序之间出现文件名冲突。 尽管具有相似名称的文件不会相互覆盖，但在故障排除过程中可能难以区分类驱动程序包文件和 v4 打印机驱动程序中的文件。

 
有关 v4 打印机驱动程序清单指令的详细信息，请参阅 [V4 驱动程序清单](v4-driver-manifest.md)。

## <a name="related-topics"></a>相关主题

[V4 驱动程序清单](v4-driver-manifest.md)  



