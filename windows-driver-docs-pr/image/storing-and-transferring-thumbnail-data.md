---
title: 存储和传输缩略图数据
description: 存储和传输缩略图数据
ms.assetid: 4c27f93f-859e-42e3-95ea-9bfd8d0329d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f335c71319863582f9477e1c619a075cfcc6217
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358240"
---
# <a name="storing-and-transferring-thumbnail-data"></a>存储和传输缩略图数据





由三个 WIA 属性控制 WIA 缩略图的信息：[**WIA\_IPC\_缩略图**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-thumbnail)， [ **WIA\_IPC\_缩略图\_宽度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-thumbnail-width)，和[ **WIA\_IPC\_缩略图\_高度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipc-thumbnail-height)。 在 Windows Me，并在 Windows XP 及更高版本，缩略图的数据是 24 位每像素只有。

<a href="" id="wia-ipc-thumbnail"></a>WIA\_IPC\_缩略图  
属性包含缩略图 RGB 格式数据，使用每像素 24 位和 32 位边界上对齐。

<a href="" id="wia-ipc-thumb-width"></a>WIA\_IPC\_THUMB\_宽度  
属性包含缩略图宽度，以像素为单位。

<a href="" id="wia-ipc-thumbnail-height"></a>WIA\_IPC\_缩略图\_高度  
属性包含缩略图高度，以像素为单位。

应用程序读取 WIA\_IPC\_THUMB\_宽度和 WIA\_IPC\_THUMB\_高度属性创建属性 BITMAPINFOHEADER 结构 （在 Microsoft 中所述Windows SDK 文档）。 然后，应用程序读取 WIA\_IPC\_缩略图的实际数据的缩略图属性。 缩略图的数据应该是未压缩，32 位边界上对齐 24 位 / 像素数据。

 

 




