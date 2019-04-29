---
title: 安装 IDE 控制器微型驱动程序
description: 安装 IDE 控制器微型驱动程序
ms.assetid: c1b41f89-150d-47e9-9bed-04f5796f69bd
keywords:
- IDE 控制器微型驱动程序 WDK 存储，安装
- 存储 IDE 控制器微型驱动程序 WDK，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 984e040b1b7d48ba59f136f727624a671bdaa235
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368790"
---
# <a name="installing-ide-controller-minidrivers"></a>安装 IDE 控制器微型驱动程序


## <span id="ddk_installing_ide_controller_minidrivers_kg"></span><span id="DDK_INSTALLING_IDE_CONTROLLER_MINIDRIVERS_KG"></span>


本部分提供特定于 IDE 控制器驱动程序和控制器微型驱动程序在 Microsoft Windows 2000 和更高版本操作系统的安装信息。

供应商提供其自己的控制器微型驱动程序应使该驱动程序中的硬盘控制器 (HDC) 安装程序类的成员[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)的驱动程序的 INF 文件。 例如：

```cpp
[version]
Signature="$WINDOWS NT$"
Class=hdc
ClassGuid={4D36E96A-E325-11CE-BFC1-08002BE10318}
```

不没有与安装 IDE 控制器微型驱动程序相关联的任何其他特殊的要求。

安装的详细信息，包括控制器支持的硬件列表在 Windows 2000 和更高版本的操作系统，请参阅硬盘控制器的系统提供 INF 文件*mshdc.inf*。

有关在 Windows 2000 和更高版本操作系统的设备安装的常规信息，请参阅[Vendor-Supplied IDE 控制器微型驱动程序的要求](requirements-for-vendor-supplied-ide-controller-minidrivers.md)并[设备安装概述](https://msdn.microsoft.com/library/windows/hardware/ff549455)。

 

 




