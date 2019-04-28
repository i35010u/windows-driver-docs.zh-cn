---
title: 支持 CMYK 色彩空间
description: 支持 CMYK 色彩空间
ms.assetid: b8ac5f1a-c903-4313-b7de-0335f4c44367
keywords:
- CMYK 颜色空间 WDK 打印
- BR_CMYKCOLOR
- XO_FROM_CMYK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 519d8de97a7d8c70cf553b5b6eaa1db9d5ee707d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331758"
---
# <a name="supporting-cmyk-color-space"></a>支持 CMYK 色彩空间





而不考虑是否颜色管理是正在处理的应用程序、 系统、 驱动程序或设备，打印机图形 DLL 颜色空间。 这是通过设置 GCAPS\_CMYKCOLOR 标志[ **DEVINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff552835)结构。 如果设置此标志和 CMYK 配置文件正在使用中，GDI 将 CMYK 颜色数据，而不是 RGB 数据发送到打印机图形 DLL 的位图、 画笔和钢笔中。 GDI 还会设置以下标志：

-   BR\_CMYKCOLOR 标志**flColorType**的成员[ **BRUSHOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff538261)结构。

-   XO\_FROM\_CMYK 标志**flXlate**的成员[ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)结构。

请注意，是否该驱动程序支持 CMYK 颜色空间，它还必须支持半色调。 因此如果驱动程序设置 GCAPS\_CMYKCOLOR 标志在 DEVINFO，它必须设置 GCAPS\_半色调。

 

 




