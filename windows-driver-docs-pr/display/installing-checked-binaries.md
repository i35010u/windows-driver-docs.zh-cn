---
title: 安装已检查的二进制文件
description: 安装已检查的二进制文件
ms.assetid: a289206a-e793-48a6-875c-f0204edfaaf3
keywords:
- 已检查二进制文件 WDK 显示
- WDK 的二进制文件显示
- 免费的二进制文件 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a6c9beb6395f17a2cd5c225231a0c22357bf846
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365460"
---
# <a name="installing-checked-binaries"></a>安装已检查的二进制文件


在开发新的驱动程序的 Windows 显示器驱动程序模型 (WDDM) 时，应使用选中的 WDDM 组件的二进制文件。 这些组件的检查二进制文件版本具有大量验证和调试辅助程序，它不适用于免费二进制文件。 但是，可用的二进制文件应该用于性能优化，因为检查二进制文件时速度慢。

硬件供应商想要为 WDDM 运行选中的二进制文件可以使用以下方法之一：

-   安装检查二进制文件版本的 Windows Vista 或更高版本。 例如，如果你要为 Windows 7 而不是 Windows Vista 开发驱动程序安装检查二进制文件版本的 Windows 7。

    这是最简单的方法。 但是，运行所有检查二进制文件版本的操作系统组件可能会导致整体性能不佳。 因此，这并不总是适当选择。

-   通过免费二进制文件版本的 Windows Vista 或更高版本安装 WDDM 组件检查二进制文件版本。

    这是建议的方法，以运行适用于 WDDM 的二进制文件。

    通过重新启动使用备用安装的 Windows Vista 或更高版本来替换 WDDM 二进制文件在免费二进制 Windows Vista 或更高版本使用它们检查二进制文件的版本。

    **请注意**   *Win32k.sys*， *Gdi32.dll*， *Winsrv.dll*，并*User32.dll*WDDM 的二进制文件此规则的例外情况。 这些二进制文件应与要安装的操作系统生成的类型始终匹配。 因此，操作系统的免费二进制版本，这些二进制文件应该也是免费的二进制文件;操作系统内部版本的检查二进制文件版本，这些二进制文件应该是选中的二进制文件。 否则为硬件供应商可以混合和匹配的所有其他 WDDM 二进制文件的免费二进制文件和检查二进制版本。

     

 

 





