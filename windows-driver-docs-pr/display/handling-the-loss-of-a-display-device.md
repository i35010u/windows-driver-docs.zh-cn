---
title: 处理显示设备的丢失
description: 处理显示设备的丢失
ms.assetid: 7af8d7e6-733d-4976-a516-7b41fa74dd5d
keywords:
- OPM WDK 显示，设备丢失
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2982b41a12f40ac495ae6411b47f950ea5e82465
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066702"
---
# <a name="handling-the-loss-of-a-display-device"></a>处理显示设备的丢失


以下方案启动对显示微型端口驱动程序的 [**DxgkDdiOPMDestroyProtectedOutput**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output) 函数的调用，同时可以启用对图形适配器的输出连接器的内容保护：

-   更改显示模式

-   从 Windows 桌面附加或分离监视器

-   输入全屏 "命令提示符" 窗口

-   启动任何 DirectDraw 或 Direct3D 专用模式应用程序

-   执行快速用户切换

-   锁定工作站或按 CTRL + ALT + DELETE

-   使用远程桌面连接连接到工作站

-   进入节能模式-例如，"挂起" 或 "休眠"

-   意外终止应用程序--例如，通过页错误

 

