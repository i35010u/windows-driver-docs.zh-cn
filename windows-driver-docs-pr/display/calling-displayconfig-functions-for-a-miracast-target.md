---
title: 对 Miracast 目标调用 DisplayConfig 函数
ms.assetid: D408986B-B33B-4A96-B93C-2A2F301E74AF
description: 对 Miracast 目标调用 DisplayConfig 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e56aa2352a7f8d6a64208b8af4c5866a40d8c8e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384606"
---
# <a name="calling-displayconfig-functions-for-a-miracast-target"></a>对 Miracast 目标调用 DisplayConfig 函数


若要减少到支持 Miracast 的新目标，公开的现有应用程序的兼容性问题[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)并[ **SetDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)函数实现具有应用，从而查找 Miracast 目标的方法：

-   值为**DISPLAYCONFIG\_输出\_技术\_MIRACAST**中[ **DISPLAYCONFIG\_视频\_输出\_技术**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)枚举指示 VidPN 目标为 Miracast 设备。
-   Flags 参数值的**QDC\_所有\_路径**对的调用中[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)不会返回连接到支持 Miracast 的任何路径不具有附加的活动监视器的目标。
-   为已连接的 Miracast 监视器，每个路径[ **QueryDisplayConfig** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig) Miracast 接收器返回报告的连接器类型。 内部 Miracast 接收器报告的值**DISPLAYCONFIG\_输出\_技术\_MIRACAST**中[ **DISPLAYCONFIG\_视频\_输出\_技术**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)枚举。 例如，如果 Miracast 接收器报告是否电视已连接到接收器使用高清晰度多媒体接口 (HDMI) 电缆，然后**QueryDisplayConfig**将报告作为目标类型**DISPLAYCONFIG\_输出\_技术\_HDMI**。
-   [ **DISPLAYCONFIG\_视频\_信号\_信息**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)结构有一个垂直同步频率分隔符成员， **vSyncFreqDivider**，类似于使用[ **D3DKMDT\_视频\_信号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)。**vSyncFreqDivider**。
-   [ **DisplayConfigGetDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)函数提供的基本连接符类型的任何目标。 对于 Miracast 目标，此函数始终返回的值**DISPLAYCONFIG\_输出\_技术\_MIRACAST**中[ **DISPLAYCONFIG\_视频\_输出\_技术**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)枚举。

 

 





