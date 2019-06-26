---
title: 处理显示设备的丢失
description: 处理显示设备的丢失
ms.assetid: 7af8d7e6-733d-4976-a516-7b41fa74dd5d
keywords:
- OPM WDK 显示、 设备丢失
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f2122928103ca266e6f1df63dfcf770824f87b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369837"
---
# <a name="handling-the-loss-of-a-display-device"></a>处理显示设备的丢失


以下方案启动显示微型端口驱动程序调用[ **DxgkDdiOPMDestroyProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)工作连接器可能会输出图形适配器上的内容保护已启用：

-   更改显示模式

-   附加或分离从 Windows 桌面监视器

-   输入的全屏命令提示符窗口

-   启动任何 DirectDraw 或 Direct3D 的排他模式应用程序

-   执行快速用户切换

-   锁定工作站或按 CTRL + ALT + DELETE

-   通过使用远程桌面连接到工作站附加

-   进入节能模式-例如，挂起或休眠状态

-   应用程序意外终止-例如，通过页面错误

 

 





