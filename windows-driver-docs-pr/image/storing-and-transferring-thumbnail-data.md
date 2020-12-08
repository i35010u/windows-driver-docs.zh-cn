---
title: 存储和传输缩略图数据
description: 存储和传输缩略图数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98a7f0f9d6e5303be4ead74053db8ec037a32dc5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838583"
---
# <a name="storing-and-transferring-thumbnail-data"></a>存储和传输缩略图数据





WIA 缩略图信息由三个 WIA 属性控制： [**WIA \_ ipc \_ 缩略图**](./wia-ipc-thumbnail.md)、 [**wia \_ ipc \_ 缩略图 \_ 宽度**](./wia-ipc-thumbnail-width.md)和 [**WIA \_ ipc \_ 缩略图 \_ 高度**](./wia-ipc-thumbnail-height.md)。 在 Windows Me 和 Windows XP 及更高版本中，缩略图数据仅为24位/像素。

<a href="" id="wia-ipc-thumbnail"></a>WIA \_ IPC \_ 缩略图  
属性包含 RGB 格式的缩略图数据，其中每像素24位，并在32位边界上对齐。

<a href="" id="wia-ipc-thumb-width"></a>WIA \_ IPC \_ 拇指 \_ 宽度  
属性包含缩略图的宽度（以像素为单位）。

<a href="" id="wia-ipc-thumbnail-height"></a>WIA \_ IPC \_ 缩略图 \_ 高度  
属性包含缩略图的高度（以像素为单位）。

应用程序将读取 "WIA \_ ipc \_ 拇指宽度" 和 " \_ wia \_ ipc \_ thumb \_ 高度" 属性，以创建 Microsoft Windows SDK 文档)  (描述的属性 BITMAPINFOHEADER 结构。 然后，应用程序将读取 \_ 实际缩略图数据的 WIA IPC \_ 缩略图属性。 缩略图数据应为非压缩缩略图，每像素数据在32位边界上对齐。

 

