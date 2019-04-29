---
title: WIA 项属性和位置更改
description: WIA 项属性和位置更改
ms.assetid: 4e8b3d2a-a28c-41d1-9c4b-8d85f28cf904
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc3b7b622b1070bfcc29828839480a50a6f83da3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352693"
---
# <a name="wia-item-property-and-location-changes"></a>WIA 项属性和位置更改





确保在 Windows Vista 和早期版本的操作系统中的应用程序兼容性的最简单方法是在 Windows XP 和 Windows Me 位置实现 WIA 属性*和*在 Windows Vista 的位置。 通常情况下，为 Windows Vista 编写的 WIA 应用程序仅能使用 WIA 属性和添加适用于 Windows Vista 编写的应用程序适用于 Windows XP 和 Windows Me 中使用时仅 WIA 属性和位置的位置在这些操作系统中定义。 在这两个位置中实现属性允许应用程序编写的 Windows Vista、 Windows XP 和 Windows 我能够使用相同的属性集实现。

在 Windows Vista 之前的操作系统，位于以下 WIA 属性的支持平板辊扫描的扫描仪驱动程序的根项。 在 Windows Vista 中，它们位于平板项上。

-   [**WIA\_DPS\_水平\_平台\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551399) (称为[ **WIA\_IP\_MAX\_水平\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff552607) Windows Vista 中)

-   [**WIA\_DPS\_垂直\_平台\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff551445) (称为[ **WIA\_IP\_MAX\_垂直\_大小**](https://msdn.microsoft.com/library/windows/hardware/ff552611) Windows Vista 中)

-   [**WIA\_DPS\_光学\_XRES** ](https://msdn.microsoft.com/library/windows/hardware/ff551409) (称为[ **WIA\_IP\_光学\_XRES** ](https://msdn.microsoft.com/library/windows/hardware/ff552620)Windows Vista 中)

-   [**WIA\_DPS\_光学\_YRES** ](https://msdn.microsoft.com/library/windows/hardware/ff551410) (称为[ **WIA\_IP\_光学\_YRES** ](https://msdn.microsoft.com/library/windows/hardware/ff552622)Windows Vista 中)

-   [**WIA\_DPS\_预览版**](https://msdn.microsoft.com/library/windows/hardware/ff551422) (称为[ **WIA\_IP\_预览**](https://msdn.microsoft.com/library/windows/hardware/ff552643) Windows Vista 中)

-   [**WIA\_DPS\_显示\_预览\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff551432) (称为[ **WIA\_IP\_显示\_预览\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff552652) Windows Vista 中)

**请注意**  重复的 WIA 属性需要仅对支持平板辊扫描或文档送纸器扫描的扫描仪。 配对的属性具有相同的属性标识符的兼容性。 该驱动程序可以添加 WIA\_DPS\_*Xxx*属性的根项和 WIA\_IP\_*Xxx*其他项。

 

 

 




