---
title: 处理 COPP 设备丢失
description: 处理 COPP 设备丢失
ms.assetid: 7e74b249-34be-44cc-a022-ba6574f2f841
keywords:
- 复制保护 WDK COPP，设备丢失
- 视频复制保护 WDK COPP，设备丢失
- COPP WDK DirectX VA，设备丢失
- 受保护的视频 WDK COPP，设备丢失
- 丢失的 COPP 设备 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 817eb16947f818eb56c93011407f7bed43029345
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065610"
---
# <a name="handling-the-loss-of-a-copp-device"></a>处理 COPP 设备丢失


## <span id="ddk_handling_the_loss_of_a_copp_device_gg"></span><span id="DDK_HANDLING_THE_LOSS_OF_A_COPP_DEVICE_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

设置为 "保护模式" 的视频会话必须处理导致 DirectX VA COPP 设备（与视频会话相关）的破坏的情况。 以下方案启动对显示驱动程序的 [*DdMoCompDestroy*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy) 回调函数的调用，同时可能会启用视频会话的经过认证的输出连接器上的内容保护：

-   更改显示模式

-   从 Windows 桌面附加或分离监视器

-   输入全屏 "命令提示符" 窗口

-   启动任何 DirectDraw 或 Direct3D 专用模式应用程序

-   执行快速用户切换

-   锁定工作站或按 CTRL + ALT + DELETE

-   使用远程桌面连接连接到工作站

-   进入节能模式-例如，"挂起" 或 "休眠"

-   意外终止应用程序--例如，通过页错误

如果在启用视频会话的 "输出内容保护" 时出现上述情况之一，则显示驱动程序的 *DdMoCompDestroy* 函数应启动对视频微型端口驱动程序的 [*COPPCloseVideoSession*](./coppclosevideosession.md) 函数的调用，以根据 COPP 设备的当前本地保护级别计数来减小全局保护级别计数。 然后，视频微型端口驱动程序应检查修改后的全局保护级别，并相应地调整应用到输出连接器的保护级别。

 

