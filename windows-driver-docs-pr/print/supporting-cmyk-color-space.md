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
ms.openlocfilehash: db31c197d4589e19d4f344ed953888cf09dacff9
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802363"
---
# <a name="supporting-cmyk-color-space"></a>支持 CMYK 色彩空间





无论应用程序、系统、驱动程序或设备是否正在处理颜色管理，打印机图形 DLL 的颜色空间都是如此。 这是通过 \_ 在 [**lnk-devinfo**](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-tagdevinfo) 结构中设置 GCAPS CMYKCOLOR 标志来完成的。 如果设置了此标志并使用了 CMYK 配置文件，则 GDI 会将 CMYK 颜色数据（而不是 RGB 数据）发送到位图、画笔和笔的打印机图形 DLL。 GDI 还设置以下标志：

-   \_ [**BRUSHOBJ**](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-_brushobj)结构的**FLCOLORTYPE**成员中的 BR CMYKCOLOR 标志。

-   \_ \_ [**XLATEOBJ**](https://docs.microsoft.com/windows/win32/api/winddi/ns-winddi-_xlateobj)结构的**flXlate**成员中的来自 CMYK 标志的 XO。

请注意，如果驱动程序支持 CMYK 颜色空间，则它还必须支持半色调。 因此，如果驱动程序 \_ 在 lnk-devinfo 中设置 GCAPS CMYKCOLOR 标志，还必须设置 GCAPS \_ 半色调。

 

 




