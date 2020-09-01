---
title: 驱动程序控制和设备控制
description: 驱动程序控制和设备控制
ms.assetid: ff515e88-9a94-420f-a6c8-fba3483c00e5
keywords:
- 专有颜色管理 WDK 打印
- DrvIcmCreateColorTransform
- 驱动程序控制的颜色管理 WDK 打印
- 设备控制的颜色管理 WDK 打印
- 驱动程序颜色管理 WDK 请参阅颜色管理 WDK
- 设备颜色管理 WDK 请参阅颜色管理 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23de368c56bb23a16ac46ee3a8205033686b23c8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217767"
---
# <a name="driver-control-and-device-control"></a>驱动程序控制和设备控制





如果颜色管理控制由驱动程序或打印机硬件提供，则驱动程序的 [打印机图形 DLL](printer-graphics-dll.md) 必须 \_ 在 [**LNK-DEVINFO**](/windows/win32/api/winddi/ns-winddi-tagdevinfo) 结构中设置 GCAPS ICM 标志。

如果适当) ，驱动程序必须指示支持 CYMK 颜色空间 (如 [支持 CMYK 颜色空间](supporting-cmyk-color-space.md)中所述。

打印机图形 Dll 必须定义以下三个函数：

[**DrvIcmCreateColorTransform**](/windows/win32/api/winddi/nf-winddi-drvicmcreatecolortransform)

[**DrvIcmDeleteColorTransform**](/windows/win32/api/winddi/nf-winddi-drvicmdeletecolortransform)

[**DrvIcmCheckBitmapBits**](/windows/win32/api/winddi/nf-winddi-drvicmcheckbitmapbits)

GDI 将调用 [**DrvIcmCreateColorTransform**](/windows/win32/api/winddi/nf-winddi-drvicmcreatecolortransform) 函数来为驱动程序提供 ICC 配置文件， (打印作业的 Microsoft Windows SDK 文档) 中所述。 对于这些配置文件，函数可创建在更正颜色信息时要使用的内部颜色转换。 颜色转换是特定于驱动程序的、内部定义的从一种颜色空间到另一颜色空间的映射。 该函数返回 GDI 存储的转换的句柄。

[**BRUSHOBJ**](/windows/win32/api/winddi/ns-winddi-_brushobj)和[**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-_xlateobj)结构中的标志指示系统 (或应用程序) 或驱动程序 (或设备) 是否正在执行颜色管理。 在每个驱动程序实现的图形 DDI 绘图函数内，该函数同时接收这些结构的 (或二者) ，必须检查标志。 如果系统或应用程序当前正在处理颜色管理，则驱动程序或设备不能。 如果启用了驱动程序或设备颜色管理，则图形 DDI 函数必须调用 [**BRUSHOBJ \_ HGetColorTransform**](/windows/win32/api/winddi/nf-winddi-brushobj_hgetcolortransform) 或 [**XLATEOBJ \_ hGetColorTransform**](/windows/win32/api/winddi/nf-winddi-xlateobj_hgetcolortransform) (或两者均) ，以获取要使用的颜色转换的句柄。 该句柄将为驱动程序提供的，以响应对其 [**DrvIcmCreateColorTransform**](/windows/win32/api/winddi/nf-winddi-drvicmcreatecolortransform) 函数的以前调用。

### <a name="handling-proprietary-color-management"></a>处理专有颜色管理

对于某些设备，无论是否启用了 ICM，都可以 (驱动程序或硬件) 执行专有颜色管理。 如果收到的图像数据已经更正，此类设备的驱动程序不得允许执行颜色更正。 如果出现以下情况，则可以接收 Precorrected 数据：

-   应用程序已将图像的颜色更正为 "DC 外" (参阅 Microsoft Windows SDK 文档) "。

-   系统正在处理颜色管理。

对于这两种情况，都将 \_ \_ 设置[**BRUSHOBJ**](/windows/win32/api/winddi/ns-winddi-_brushobj)的**flColorType**成员中的 BR 主机 icm 标志和 \_ \_ [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-_xlateobj)的**flXlate**成员中的 XO 主机 icm 标志。 即使[**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew)的**DMICMMETHOD**成员为 dmICMMethod NONE，也可以设置这些标志 \_ 。

 

