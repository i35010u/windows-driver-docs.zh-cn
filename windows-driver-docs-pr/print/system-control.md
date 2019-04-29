---
title: 系统控制
description: 系统控制
ms.assetid: 3ac58d53-daa7-4f50-a512-05325b95a17d
keywords:
- 系统控制颜色管理 WDK 打印
- 默认打印颜色管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11b4d2db6950f4089a4182af17289b40cf391212
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387810"
---
# <a name="system-control"></a>系统控制





系统控制颜色管理是默认颜色管理类型。 它也是建议的打印机类型。 如果启用了颜色管理，GDI 纠正了所有 Dib，笔的颜色，然后将它们发送到驱动程序的打印机图形 DLL，根据输入和输出的画笔颜色空间和安装 ICC 配置文件。

没有特定于 ICM 的代码需要添加到的打印机驱动程序支持系统控制颜色管理，以外，该值指示对 CYMK 颜色空间 （如果适用），如中所述的支持[支持 CMYK 颜色空间](supporting-cmyk-color-space.md)。

 

 




