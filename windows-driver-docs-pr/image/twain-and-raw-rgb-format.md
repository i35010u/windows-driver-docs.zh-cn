---
title: TWAIN 和原始 RGB 格式
description: TWAIN 和原始 RGB 格式
ms.assetid: 0de4a547-6c8e-4fbf-a7a3-7af440bf72f3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d691b11c1ff1c842d0c53606f8a36114233655e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379830"
---
# <a name="twain-and-raw-rgb-format"></a>TWAIN 和原始 RGB 格式





应用程序时将映像传输其格式的 GUID 是 WiaImgFmt\_RAWRGB (标头文件中定义*wiadef.h*)，在图像上的以下属性必须包含的图像的正确值：

-   WIA\_IPA\_CHANNELS\_PER\_PIXEL

-   WIA\_IPA\_BITS\_每\_通道

-   WIA\_IPA\_PIXELS\_PER\_LINE

-   WIA\_IPA\_数\_OF\_行

-   WIA\_IPS\_XRES

-   WIA\_IP\_YRES

此外，WIA\_IPA\_数据类型属性应设置为 WIA\_数据\_颜色和 WIA\_IPA\_DEPTH 属性应设置为 24 或更高版本。 有关这些属性的详细信息，请参阅 Microsoft Windows SDK 文档。

要传输的原始 RGB 格式中的任何数据必须是：

-   未压缩

-   RGB 字节顺序排列

-   双字节边界上对齐

必须使用无映像标头传输数据。 **IWiaDataCallback::BandedDataCallback**方法 （Windows SDK 文档中所述） 会发送仅图像位。

TWAIN 兼容性层 (请参阅[TWAIN 兼容应用程序的支持](support-for-twain-compatible-applications.md)) 支持 WiaImgFmt\_RAWRGB 格式的 GUID。 这样，TWAIN 应用程序将使用像素深度大于 32 位，使用内存回调传输映像传输。

 

 




