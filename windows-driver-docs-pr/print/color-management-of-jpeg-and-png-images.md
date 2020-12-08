---
title: JPEG 和 PNG 图像的颜色管理
description: JPEG 和 PNG 图像的颜色管理
keywords:
- JPEG 彩色管理 WDK 打印
- PNG 颜色管理 WDK 打印
- CHECKJPEGFORMAT
- CHECKPNGFORMAT
- 压缩的图像 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2e17793509feb6cc0d72bfddf4186cb99f1af47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797686"
---
# <a name="color-management-of-jpeg-and-png-images"></a>JPEG 和 PNG 图像的颜色管理





对于提供 JPEG 和 PNG 压缩图像硬件支持的打印机，颜色管理必须由驱动程序或设备处理，且不能由 GDI 处理。

在应用程序将 JPEG 或 PNG 压缩图像发送到打印机之前，它将使用 CHECKJPEGFORMAT 或 CHECKPNGFORMAT 转义代码调用 ExtEscape。 这会导致调用驱动程序的 [**DrvQueryDeviceSupport**](/windows/win32/api/winddi/nf-winddi-drvquerydevicesupport) 函数，其查询类型为 QDS \_ CHECKJPEGFORMAT 或 QDS \_ CHECKPNGFORMAT，以及包含压缩映像的缓冲区。

驱动程序可以检查图像数据并确定它是否可以支持映像。 如果设置了 [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-xlateobj) 结构的 XO \_ 设备 \_ icm 标志或 XO 主机 ICM 标志，则支持映像必须包括执行颜色转换 \_ \_ ，因为 GDI 无法对此类图像执行颜色转换。

对于这些压缩映像，颜色空间信息通常包含在图像数据中。 一个例外是 JFIF 文件，这些文件是 YCbCr 编码的，默认的 sRGB 空间是良好的近似值。 但是，JFIF 文件可能包含专用的应用 *x* 标记，该标记指定了颜色空间，在这种情况下，驱动程序必须使用颜色空间来转换图像。

有关支持 JPEG 和 PNG 压缩映像的详细信息，请参阅 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)的 "备注" 部分。

 

