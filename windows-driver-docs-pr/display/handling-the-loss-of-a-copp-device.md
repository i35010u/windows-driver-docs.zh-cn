---
title: 处理 COPP 设备丢失
description: 处理 COPP 设备丢失
ms.assetid: 7e74b249-34be-44cc-a022-ba6574f2f841
keywords:
- 复制保护 WDK COPP，丢失的设备
- 视频复制保护 WDK COPP，丢失的设备
- COPP WDK DirectX va，因此丢失的设备
- 受保护视频 WDK COPP，丢失的设备
- 丢失的 COPP 设备 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 106d12ef7ff8282e24046a6b09f92a41e30483fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363769"
---
# <a name="handling-the-loss-of-a-copp-device"></a>处理 COPP 设备丢失


## <span id="ddk_handling_the_loss_of_a_copp_device_gg"></span><span id="DDK_HANDLING_THE_LOSS_OF_A_COPP_DEVICE_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

设置为受保护模式的视频会话必须处理导致 DirectX VA COPP 设备与视频会话相关联的析构的方案。 以下方案启动显示器驱动程序调用[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)回调函数时可能是视频会话认证的输出连接器上的内容保护已启用：

-   更改显示模式

-   附加或分离从 Windows 桌面监视器

-   输入的全屏命令提示符窗口

-   启动任何 DirectDraw 或 Direct3D 的排他模式应用程序

-   执行快速用户切换

-   锁定工作站或按 CTRL + ALT + DELETE

-   通过使用远程桌面连接到工作站附加

-   进入节能模式-例如，挂起或休眠状态

-   应用程序意外终止-例如，通过页面错误

如果在前面的方案之一时发生输出内容保护为视频会话启用之后，显示驱动程序*DdMoCompDestroy*函数应启动微型端口驱动程序的调用[ *COPPCloseVideoSession* ](https://msdn.microsoft.com/library/windows/hardware/ff539638)函数以减少 COPP 设备的当前本地保护级别计数将全局保护级别计数。 然后，微型端口驱动程序应检查修改后的全局保护级别，并调整相应地应用于输出连接器的保护级别。

 

 





