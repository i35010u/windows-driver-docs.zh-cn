---
title: 桌面布局
description: 桌面布局
ms.assetid: f1c074ec-2fce-4e46-ba0d-62e05ca8a9e7
keywords:
- 连接显示 WDK Windows 7 显示、 CCD 概念、 桌面设备布局
- 连接显示 WDK Windows Server 2008 R2 显示、 CCD 概念、 桌面设备布局
- 配置显示 WDK Windows 7 显示、 CCD 概念、 桌面设备布局
- 配置显示 WDK Windows Server 2008 R2 显示、 CCD 概念、 桌面设备布局
- CCD 概念 WDK Windows 7 显示、 桌面设备布局
- CCD 概念 WDK Windows Server 2008 R2 显示、 桌面设备布局
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdfd97e2b5408fbb44af889f8c64a36c5a7155cc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567139"
---
# <a name="desktop-layout"></a>桌面布局


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

调用方将使用**位置**的成员[ **DISPLAYCONFIG\_源\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff553986)对的调用中的结构[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533) CCD 函数来控制源的排列方式显示在桌面上。 **位置**成员指定的源图面左上角以桌面坐标位置。 位于源图面 （0，0） 是考虑主图面。 GDI 具有严格的规则，有关桌面空间中的源图面可以排列方式。 例如，GDI 不允许源图面中的源图面之间没有重叠空白。

尽管[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)尝试重新排列源代码的图面以强制实施这些 GDI 布局规则、 调用方应指定的源图面布局。 它未定义 GDI 重新强制执行其布局规则，将源曲面的排列，且生成的源图面布局可能不是调用方想要在实现。

 

 





