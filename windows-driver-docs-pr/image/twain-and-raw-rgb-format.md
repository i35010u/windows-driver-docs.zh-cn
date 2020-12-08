---
title: TWAIN 和原始 RGB 格式
description: TWAIN 和原始 RGB 格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 265b1df36a9c8630bda13f82e57ceb5c6ba68bae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819541"
---
# <a name="twain-and-raw-rgb-format"></a>TWAIN 和原始 RGB 格式





当应用程序传输其格式 GUID 为 WiaImgFmt \_ RAWRGB (在头文件 *wiadef*) 中定义的图像时，映像上的以下属性必须包含正确的映像值：

-   WIA \_ IPA \_ \_ 每像素通道数 \_

-   WIA \_ \_ \_ 每通道 IPA 位数 \_

-   WIA \_ \_ \_ 每行 IPA 像素 \_

-   WIA \_ IPA \_ \_ 行数 \_

-   WIA \_ IP \_ XRES

-   WIA \_ IP \_ YRES

此外，WIA \_ IPA 数据 \_ 类型属性应设置为 WIA \_ 数据 \_ 颜色，并且 wia \_ IPA \_ DEPTH 属性应设置为24或更高。 有关这些属性的详细信息，请参阅 Microsoft Windows SDK 文档。

要传输的原始 RGB 格式的任何数据必须为：

-   未压缩

-   按 RGB 字节顺序排列

-   对齐 DWORD 边界

数据必须传输，无图像标头。 Windows SDK 文档中所述的 **IWiaDataCallback：： BandedDataCallback** 方法 () 只发送图像位。

TWAIN 兼容层 (请参阅 [对 TWAIN-Compatible 应用程序的支持](support-for-twain-compatible-applications.md)) 支持 WiaImgFmt \_ RAWRGB 格式 GUID。 这使得 TWAIN 应用程序能够使用内存回调传输来传输像素深度大于32位的图像。

 

 




