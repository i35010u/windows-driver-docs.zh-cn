---
title: 为打印机创建属性表页
description: 为打印机创建属性表页
ms.assetid: b9b7aa52-39b7-4809-acdf-e72293da37e1
keywords:
- 打印机接口 DLL WDK，属性表页
- 属性表页 WDK 打印创建
- 属性表页 WDK 打印，打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1d1d3bc62f20a478d5cf7d13654eec3657b8786
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390933"
---
# <a name="creating-property-sheet-pages-for-printers"></a>为打印机创建属性表页





打印机接口 dll 函数，结合[CPSUI](common-property-sheet-user-interface.md)、 负责创建该用户的 Windows 2000 的属性表页和更高版本用于查看和修改与打印机相关联的配置参数和打印文档数。 DLL 必须提供每个打印机接口[ **DrvDevicePropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff548542)函数来创建特定于打印机的页面和一个[ **DrvDocumentPropertySheets**](https://msdn.microsoft.com/library/windows/hardware/ff548548)函数来创建特定于文档的页。

若要了解应如何设计这些函数，请务必阅读部分描述[CPSUI](common-property-sheet-user-interface.md)。 显示属性表页涉及应用程序、 打印后台处理程序、 打印机接口 DLL，以及 CPSUI 之间的交互。 中介绍了执行流[与打印机驱动程序使用 CPSUI](using-cpsui-with-printer-drivers.md)。

 

 




