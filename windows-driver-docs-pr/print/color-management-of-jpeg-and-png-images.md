---
title: JPEG 和 PNG 图像的颜色管理
description: JPEG 和 PNG 图像的颜色管理
ms.assetid: ece0578d-bf03-4eee-9568-40ef684ba8a7
keywords:
- JPEG 颜色管理 WDK 打印
- PNG 颜色管理 WDK 打印
- CHECKJPEGFORMAT
- CHECKPNGFORMAT
- 压缩的映像 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be74cf5573c2ea74c487a64cabf8a096e48cb39d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351911"
---
# <a name="color-management-of-jpeg-and-png-images"></a>JPEG 和 PNG 图像的颜色管理





对于提供硬件支持的 JPEG 和 PNG 压缩映像的打印机，颜色管理必须处理由驱动程序或设备，不能通过 GDI 进行处理。

应用程序发送到打印机的 JPEG 或 PNG 的压缩的映像之前，它将调用 ExtEscape 使用 CHECKJPEGFORMAT 或 CHECKPNGFORMAT 转义码。 这会导致驱动程序的调用[ **DrvQueryDeviceSupport** ](https://msdn.microsoft.com/library/windows/hardware/ff556260)函数，查询类型的任一 QDS\_CHECKJPEGFORMAT 或 QDS\_CHECKPNGFORMAT 和缓冲区包含压缩的映像。

该驱动程序可以检查图像数据，并确定它是否可以支持图像。 支持映像必须包括执行颜色转换，如果任一[ **XLATEOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff570634)结构的 XO\_设备\_ICM 标志或 XO\_主机\_设置 ICM 标志，因为 GDI 不能对此类映像执行颜色转换。

对于这些压缩映像，颜色空间信息通常包含在图像数据。 一个例外是 JFIF 文件，这是 YCbCr 编码和为其默认 sRGB 空间是准确的估算。 但是，JFIF 文件可能包含的专有应用*x*指定颜色空间，在其中用例驱动程序必须转换使用的颜色空间的映像的标记。

详细了解支持 JPEG 和 PNG 压缩映像，请参阅备注部分[ **DEVINFO**](https://msdn.microsoft.com/library/windows/hardware/ff552835)。

 

 




