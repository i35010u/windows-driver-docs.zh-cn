---
title: 使用 WIA 项描述 WIA 设备
description: 使用 WIA 项描述 WIA 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13f42e30525c644b5f92a4e0bf26735ea330d649
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837251"
---
# <a name="describing-a-wia-device-using-wia-items"></a>使用 WIA 项描述 WIA 设备





本主题适用于 Windows Vista 和更高版本。

WIA 项可以代表 WIA 设备的可编程数据源 (例如，扫描仪的自动文档送纸器) 或存储在该设备上的数据 (例如，照相机) 上的图片。 WIA 设备应该分成单独的项目，以正确描述该设备产生的不同数据。 这里是两个示例：

<a href="" id="scanner-example"></a>**扫描器示例**  
支持平板扫描和文档送纸器扫描的 WIA 扫描器设备具有两个主要的子项。 一个子项表示平板扫描功能，另一个子项表示文档送纸器扫描功能。

<a href="" id="camera-example"></a>**相机示例**  
存储图片的 WIA 照相机设备具有表示子文件夹和图片的子项。

本部分的其余部分包含以下主题：

[WIA 项标志](wia-item-flags.md)

[WIA 项类别](wia-item-categories.md)

[WIA 项标志和类别的示例用法](example-usage-of-wia-item-flags-and-categories.md)

[WIA 根项](wia-root-item.md)

[WIA 数据项](wia-data-item.md)

 

 




