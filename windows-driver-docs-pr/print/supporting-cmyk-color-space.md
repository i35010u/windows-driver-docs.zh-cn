---
title: 支持 CMYK 色彩空间
description: 支持 CMYK 色彩空间
ms.assetid: b8ac5f1a-c903-4313-b7de-0335f4c44367
keywords:
- CMYK 色彩空间 WDK 打印
- BR_CMYKCOLOR
- XO_FROM_CMYK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dbfe674acbeab7acdc3067acb9e73d13592b8f8
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361553"
---
# <a name="supporting-cmyk-color-space"></a>支持 CMYK 色彩空间





无论应用程序、系统、驱动程序或设备是否正在处理颜色管理， [打印机图形 DLL](printer-graphics-dll.md) 都必须指示它是否支持 *CMYK* 颜色空间。 这是通过 \_ 在 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo) 结构中设置 GCAPS CMYKCOLOR 标志来完成的。 如果设置了此标志并使用了 CMYK 配置文件，则 GDI 会将 CMYK 颜色数据（而不是 RGB 数据）发送到位图、画笔和笔的打印机图形 DLL。 GDI 还设置以下标志：

-   \_ [**BRUSHOBJ**](/windows/win32/api/winddi/ns-winddi-brushobj)结构的 **FLCOLORTYPE** 成员中的 BR CMYKCOLOR 标志。

-   \_ \_ [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-xlateobj)结构的 **flXlate** 成员中的来自 CMYK 标志的 XO。

请注意，如果驱动程序支持 CMYK 颜色空间，则它还必须支持半色调。 因此，如果驱动程序 \_ 在 lnk-devinfo 中设置 GCAPS CMYKCOLOR 标志，还必须设置 GCAPS \_ 半色调。

 

