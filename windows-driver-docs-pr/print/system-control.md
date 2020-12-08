---
title: 系统控制
description: 系统控制
keywords:
- 系统控制的颜色管理 WDK 打印
- 默认打印颜色管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c66d1c96928f22ba262461ea8490d8eaf02581c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806767"
---
# <a name="system-control"></a>系统控制





系统控制的颜色管理是默认的颜色管理类型。 这也是打印机建议的类型。 如果启用了颜色管理，则在将所有 Dib、笔和画笔的颜色发送到驱动程序的打印机图形 DLL 之前，GDI 会根据输入和输出的颜色空间和安装的 ICC 配置文件来更正这些颜色。

不需要将 ICM 特定的代码添加到打印机驱动程序来支持系统控制颜色管理，而不是指示支持 CYMK 颜色空间 (如有必要) ，如 [支持 CMYK 颜色空间](supporting-cmyk-color-space.md)中所述。

 

 




