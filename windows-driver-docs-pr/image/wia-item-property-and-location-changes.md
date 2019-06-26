---
title: WIA 项属性和位置更改
description: WIA 项属性和位置更改
ms.assetid: 4e8b3d2a-a28c-41d1-9c4b-8d85f28cf904
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60fcece6f64c27ae0e5c88f8521d6c2a2a1acdf6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355209"
---
# <a name="wia-item-property-and-location-changes"></a>WIA 项属性和位置更改





确保在 Windows Vista 和早期版本的操作系统中的应用程序兼容性的最简单方法是在 Windows XP 和 Windows Me 位置实现 WIA 属性*和*在 Windows Vista 的位置。 通常情况下，为 Windows Vista 编写的 WIA 应用程序仅能使用 WIA 属性和添加适用于 Windows Vista 编写的应用程序适用于 Windows XP 和 Windows Me 中使用时仅 WIA 属性和位置的位置在这些操作系统中定义。 在这两个位置中实现属性允许应用程序编写的 Windows Vista、 Windows XP 和 Windows 我能够使用相同的属性集实现。

在 Windows Vista 之前的操作系统，位于以下 WIA 属性的支持平板辊扫描的扫描仪驱动程序的根项。 在 Windows Vista 中，它们位于平板项上。

-   [**WIA\_DPS\_水平\_平台\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-horizontal-bed-size) (称为[ **WIA\_IP\_MAX\_水平\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-horizontal-size) Windows Vista 中)

-   [**WIA\_DPS\_垂直\_平台\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-vertical-bed-size) (称为[ **WIA\_IP\_MAX\_垂直\_大小**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-max-vertical-size) Windows Vista 中)

-   [**WIA\_DPS\_光学\_XRES** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-optical-xres) (称为[ **WIA\_IP\_光学\_XRES** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-xres)Windows Vista 中)

-   [**WIA\_DPS\_光学\_YRES** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-optical-yres) (称为[ **WIA\_IP\_光学\_YRES** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-optical-yres)Windows Vista 中)

-   [**WIA\_DPS\_预览版**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-preview) (称为[ **WIA\_IP\_预览**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-preview) Windows Vista 中)

-   [**WIA\_DPS\_显示\_预览\_控制**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-show-preview-control) (称为[ **WIA\_IP\_显示\_预览\_控制**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-show-preview-control) Windows Vista 中)

**请注意**  重复的 WIA 属性需要仅对支持平板辊扫描或文档送纸器扫描的扫描仪。 配对的属性具有相同的属性标识符的兼容性。 该驱动程序可以添加 WIA\_DPS\_*Xxx*属性的根项和 WIA\_IP\_*Xxx*其他项。

 

 

 




