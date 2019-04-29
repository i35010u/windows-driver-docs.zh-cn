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
ms.openlocfilehash: eca096b1cd3598e2da5db8434a491f6db8d4efb5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387265"
---
# <a name="driver-control-and-device-control"></a>驱动程序控制和设备控制





如果颜色管理控件是由任一驱动程序或提供打印机硬件的驱动程序[打印机图形 DLL](printer-graphics-dll.md)必须设置 GCAPS\_中的 ICM 标志[ **DEVINFO**](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构。

该驱动程序必须指示对 CYMK 颜色空间 （如果适用），如中所述的支持[支持 CMYK 颜色空间](supporting-cmyk-color-space.md)。

打印机图形 Dll 必须定义以下三个函数：

[**DrvIcmCreateColorTransform**](https://msdn.microsoft.com/library/windows/hardware/ff556239)

[**DrvIcmDeleteColorTransform**](https://msdn.microsoft.com/library/windows/hardware/ff556241)

[**DrvIcmCheckBitmapBits**](https://msdn.microsoft.com/library/windows/hardware/ff556238)

GDI 调用[ **DrvIcmCreateColorTransform** ](https://msdn.microsoft.com/library/windows/hardware/ff556239)函数来提供驱动程序使用 ICC 配置文件 （Microsoft Windows SDK 文档中所述） 打印作业。 给定这些配置文件，该函数可以创建更正颜色信息时要使用的内部颜色转换。 颜色转换为的特定于驱动程序，在内部定义从一种颜色空间映射到另一个。 该函数返回的句柄的转换，GDI 将存储。

标记内[ **BRUSHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff538261)并[ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)结构指示是否正在执行颜色管理系统 （或应用程序） 或由驱动程序 （或设备）。 在驱动程序实现的每个图形 DDI 的绘图函数接收 （或两者） 的这些结构，必须选中标志。 如果系统或应用程序当前正在处理颜色管理，驱动程序或设备都必须不。 如果启用了驱动程序或设备的颜色管理，必须调用图形 DDI 函数[ **BRUSHOBJ\_hGetColorTransform** ](https://msdn.microsoft.com/library/windows/hardware/ff538262)或[ **XLATEOBJ\_hGetColorTransform** ](https://msdn.microsoft.com/library/windows/hardware/ff570639) （或两者） 来获取要使用的颜色转换的句柄。 句柄将驱动程序的以前调用的响应中提供的其中一个其[ **DrvIcmCreateColorTransform** ](https://msdn.microsoft.com/library/windows/hardware/ff556239)函数。

### <a name="handling-proprietary-color-management"></a>处理专有颜色管理

对于某些设备，专有颜色管理是无论是否已启用 ICM 执行 （由驱动程序或硬件）。 此类设备的驱动程序必须允许颜色校正，当接收到的图像数据已更正必须执行。 如果可以接收 precorrected 的数据：

-   应用程序具有颜色校正"外部 DC"的图像 （请参阅 Microsoft Windows SDK 文档）。

-   颜色管理系统处理。

对于任一情况下，这两个 b R\_主机\_中的 ICM 标志**flColorType**的成员[ **BRUSHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff538261)和 XO\_主机\_中的 ICM 标志**flXlate**的成员[ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)将设置。 可以设置这些标志即使**dmICMMethod**的成员[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)是 DMICMMETHOD\_NONE。

 

 




