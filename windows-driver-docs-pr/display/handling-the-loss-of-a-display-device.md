---
title: 处理显示设备的丢失
description: 处理显示设备的丢失
ms.assetid: 7af8d7e6-733d-4976-a516-7b41fa74dd5d
keywords:
- OPM WDK 显示、 设备丢失
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70740e4ce89c1aaebe5b9230019826dbd51941c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366021"
---
# <a name="handling-the-loss-of-a-display-device"></a>处理显示设备的丢失


以下方案启动显示微型端口驱动程序调用[ **DxgkDdiOPMDestroyProtectedOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff559708)工作连接器可能会输出图形适配器上的内容保护已启用：

-   更改显示模式

-   附加或分离从 Windows 桌面监视器

-   输入的全屏命令提示符窗口

-   启动任何 DirectDraw 或 Direct3D 的排他模式应用程序

-   执行快速用户切换

-   锁定工作站或按 CTRL + ALT + DELETE

-   通过使用远程桌面连接到工作站附加

-   进入节能模式-例如，挂起或休眠状态

-   应用程序意外终止-例如，通过页面错误

 

 





