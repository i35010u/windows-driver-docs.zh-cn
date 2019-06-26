---
title: 驱动程序控制和设备控制
description: 驱动程序控制和设备控制
ms.assetid: ff515e88-9a94-420f-a6c8-fba3483c00e5
keywords:
- 专有颜色管理 WDK 打印
- DrvIcmCreateColorTransform
- 驱动程序控制颜色管理 WDK 打印
- 设备控制颜色管理 WDK 打印
- 请参阅 WDK 颜色管理 WDK 的驱动程序颜色管理
- 设备颜色管理请参阅 WDK 颜色管理 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cea941a3b82435bc705b2d8e2c6c94d122bef660
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383539"
---
# <a name="driver-control-and-device-control"></a>驱动程序控制和设备控制





如果颜色管理控件是由任一驱动程序或提供打印机硬件的驱动程序[打印机图形 DLL](printer-graphics-dll.md)必须设置 GCAPS\_中的 ICM 标志[ **DEVINFO**](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-tagdevinfo)结构。

该驱动程序必须指示对 CYMK 颜色空间 （如果适用），如中所述的支持[支持 CMYK 颜色空间](supporting-cmyk-color-space.md)。

打印机图形 Dll 必须定义以下三个函数：

[**DrvIcmCreateColorTransform**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform)

[**DrvIcmDeleteColorTransform**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmdeletecolortransform)

[**DrvIcmCheckBitmapBits**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcheckbitmapbits)

GDI 调用[ **DrvIcmCreateColorTransform** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform)函数来提供驱动程序使用 ICC 配置文件 （Microsoft Windows SDK 文档中所述） 打印作业。 给定这些配置文件，该函数可以创建更正颜色信息时要使用的内部颜色转换。 颜色转换为的特定于驱动程序，在内部定义从一种颜色空间映射到另一个。 该函数返回的句柄的转换，GDI 将存储。

标记内[ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)并[ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)结构指示是否正在执行颜色管理系统 （或应用程序） 或由驱动程序 （或设备）。 在驱动程序实现的每个图形 DDI 的绘图函数接收 （或两者） 的这些结构，必须选中标志。 如果系统或应用程序当前正在处理颜色管理，驱动程序或设备都必须不。 如果启用了驱动程序或设备的颜色管理，必须调用图形 DDI 函数[ **BRUSHOBJ\_hGetColorTransform** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_hgetcolortransform)或[ **XLATEOBJ\_hGetColorTransform** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-xlateobj_hgetcolortransform) （或两者） 来获取要使用的颜色转换的句柄。 句柄将驱动程序的以前调用的响应中提供的其中一个其[ **DrvIcmCreateColorTransform** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvicmcreatecolortransform)函数。

### <a name="handling-proprietary-color-management"></a>处理专有颜色管理

对于某些设备，专有颜色管理是无论是否已启用 ICM 执行 （由驱动程序或硬件）。 此类设备的驱动程序必须允许颜色校正，当接收到的图像数据已更正必须执行。 如果可以接收 precorrected 的数据：

-   应用程序具有颜色校正"外部 DC"的图像 （请参阅 Microsoft Windows SDK 文档）。

-   颜色管理系统处理。

对于任一情况下，这两个 b R\_主机\_中的 ICM 标志**flColorType**的成员[ **BRUSHOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_brushobj)和 XO\_主机\_中的 ICM 标志**flXlate**的成员[ **XLATEOBJ** ](https://docs.microsoft.com/windows/desktop/api/winddi/ns-winddi-_xlateobj)将设置。 可以设置这些标志即使**dmICMMethod**的成员[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)是 DMICMMETHOD\_NONE。

 

 




