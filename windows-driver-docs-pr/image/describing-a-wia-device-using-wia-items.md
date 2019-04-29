---
title: 使用 WIA 项描述 WIA 设备
description: 使用 WIA 项描述 WIA 设备
ms.assetid: d8149f78-e095-48f9-be79-ff115b25f14e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5df21a7249de123b39cb2a049a697ae09143be51
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373207"
---
# <a name="describing-a-wia-device-using-wia-items"></a>使用 WIA 项描述 WIA 设备





本主题适用于 Windows Vista 和更高版本。

WIA 项可以表示的可编程数据源的 WIA 设备 （例如，扫描程序的自动文档送纸器） 或该设备 （例如，摄像机上的图片） 上存储的数据。 WIA 设备应分解为各个项，以便正确地描述生成的该设备的不同数据。 下面是两个示例：

<a href="" id="scanner-example"></a>**扫描程序示例**  
支持平板扫描和文档送纸器扫描 WIA 扫描程序设备有两个主要子项目。 一个子项目表示扫描功能，平板和另一个表示文档送纸器扫描功能。

<a href="" id="camera-example"></a>**照相机示例**  
存储图片的 WIA 照相机设备具有表示子文件夹和图片的子项。

本部分的其余部分包含以下主题：

[WIA 项标志](wia-item-flags.md)

[WIA 项类别](wia-item-categories.md)

[示例用法的 WIA 项标志和类别](example-usage-of-wia-item-flags-and-categories.md)

[WIA Root Item](wia-root-item.md)

[WIA 数据项](wia-data-item.md)

 

 




