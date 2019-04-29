---
title: 启用颜色管理
description: 启用颜色管理
ms.assetid: 750d1e44-6d1c-4f18-94cb-20f1f846c0d1
keywords:
- 颜色管理 WDK 打印启用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 017426533047c12c555cd7ad5d92c4850eba10e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378618"
---
# <a name="enabling-color-management"></a>启用颜色管理





颜色管理可以启用应用程序或打印机驱动程序。 应用程序可以通过以下两种方法之一启用颜色管理：

-   调用**SetICMMode** （Microsoft Windows SDK 文档中介绍），指定 ICM\_ON。

    此方法使系统控制颜色管理。

-   指定[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构在调用时**CreateDC**创建打印作业，并设置任一 DMICMMETHOD\_系统，DMICMMETHOD\_驱动程序或 DMICMMETHOD\_DEVMODE 结构中的设备**dmICMMethod**成员。

    此方法允许应用程序选择驱动程序控制，或设备控制系统控制的颜色管理 （假定指定的控件类型支持）。

打印机驱动程序可以通过颜色管理设置任一 DMICMMETHOD\_系统、 DMICMMETHOD\_驱动程序或 DMICMMETHOD\_中的设备**dmICMMethod**的驱动程序的默认成员DEVMODE 结构。 (如果提供 DEVMODE 结构，应用程序可以重写默认设置**CreateDC**。 此外，驱动程序负责将颜色管理的用户的选择存储驱动程序的执行期间[ **DrvDocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff548548)函数。)

 

 




