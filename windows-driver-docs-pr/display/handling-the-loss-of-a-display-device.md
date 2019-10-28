---
title: 处理显示设备的丢失
description: 处理显示设备的丢失
ms.assetid: 7af8d7e6-733d-4976-a516-7b41fa74dd5d
keywords:
- OPM WDK 显示，设备丢失
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4947937f8b2bc84bc6a58250086e3ac91c88db5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839658"
---
# <a name="handling-the-loss-of-a-display-device"></a>处理显示设备的丢失


以下方案启动对显示微型端口驱动程序的[**DxgkDdiOPMDestroyProtectedOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_opm_destroy_protected_output)函数的调用，同时可以启用对图形适配器的输出连接器的内容保护：

-   更改显示模式

-   从 Windows 桌面附加或分离监视器

-   输入全屏 "命令提示符" 窗口

-   启动任何 DirectDraw 或 Direct3D 专用模式应用程序

-   执行快速用户切换

-   锁定工作站或按 CTRL + ALT + DELETE

-   使用远程桌面连接连接到工作站

-   进入节能模式-例如，"挂起" 或 "休眠"

-   意外终止应用程序--例如，通过页错误

 

 





