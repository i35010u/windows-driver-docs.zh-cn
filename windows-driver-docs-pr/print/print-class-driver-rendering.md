---
title: V4 打印类驱动程序渲染
description: 进行呈现，v4 打印机驱动程序可以利用现有的呈现功能的打印类驱动程序。
ms.assetid: F8178988-1C11-4B21-B250-6626528E0AE5
ms.date: 07/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: b9dd9fa0b4ca6576794281e6e6460b8c0ee9d2f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389480"
---
# <a name="v4-print-class-driver-rendering"></a>V4 打印类驱动程序渲染


进行呈现，v4 打印机驱动程序可以利用现有的呈现功能的打印类驱动程序。

若要利用现有的呈现功能打印类驱动程序，v4 打印机驱动程序可以使用**RequiredClass** v4 清单指令。 使用**RequiredClass**指令会导致驱动程序，包括从指定的类驱动程序，使用的设备和其 GUID 的驱动程序/友好名称作为键的所有文件。 这是用于将打印类驱动程序链接到特定于模型的打印机驱动程序的机制。

例如，通过名为打印类驱动程序为 Fabrikam 的公司*PCL5e*，可以使用下面的示例打印驱动程序清单以将其打印类驱动程序链接到其打印机驱动程序：

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
PrinterExtensionUrl="http://www.fabrikam.com/download.asp?uiapp=120"

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
> **RequiredClass**指令不能由类驱动程序。 当你使用**RequiredClass**，应避免文件之间的打印机驱动程序和打印类驱动程序所链接的名称冲突。 尽管具有类似名称的文件不会相互覆盖，但它可能很难在疑难解答期间，若要区分类驱动程序包文件和 v4 打印机驱动程序中的文件。

 
V4 打印机驱动程序清单指令的详细信息，请参阅[V4 驱动程序清单](v4-driver-manifest.md)。

## <a name="related-topics"></a>相关主题

[V4 驱动程序清单](v4-driver-manifest.md)  



