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
ms.openlocfilehash: 2bbf43a9df109d7f45213f69304622cf5a4b200a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217951"
---
# <a name="supporting-cmyk-color-space"></a>支持 CMYK 色彩空间





无论应用程序、系统、驱动程序或设备是否正在处理颜色管理，打印机图形 DLL 的颜色空间都是如此。 这是通过 \_ 在 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-tagdevinfo) 结构中设置 GCAPS CMYKCOLOR 标志来完成的。 如果设置了此标志并使用了 CMYK 配置文件，则 GDI 会将 CMYK 颜色数据（而不是 RGB 数据）发送到位图、画笔和笔的打印机图形 DLL。 GDI 还设置以下标志：

-   \_ [**BRUSHOBJ**](/windows/win32/api/winddi/ns-winddi-_brushobj)结构的**FLCOLORTYPE**成员中的 BR CMYKCOLOR 标志。

-   \_ \_ [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-_xlateobj)结构的**flXlate**成员中的来自 CMYK 标志的 XO。

请注意，如果驱动程序支持 CMYK 颜色空间，则它还必须支持半色调。 因此，如果驱动程序 \_ 在 lnk-devinfo 中设置 GCAPS CMYKCOLOR 标志，还必须设置 GCAPS \_ 半色调。

 

