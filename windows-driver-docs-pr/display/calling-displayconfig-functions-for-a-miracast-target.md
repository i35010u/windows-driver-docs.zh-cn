---
title: 对 Miracast 目标调用 DisplayConfig 函数
ms.assetid: D408986B-B33B-4A96-B93C-2A2F301E74AF
description: 对 Miracast 目标调用 DisplayConfig 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 495773c6d9da6ddb1cf63314a3755719a4b16cfc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839061"
---
# <a name="calling-displayconfig-functions-for-a-miracast-target"></a>对 Miracast 目标调用 DisplayConfig 函数


为了降低公开给新 Miracast 目标的现有应用的兼容性问题， [**QueryDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)和[**SetDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-setdisplayconfig)函数实现有多种方法可让应用查找 Miracast 目标：

-   值为**DISPLAYCONFIG\_\_技术\_MIRACAST MIRACAST** [ **\_视频\_输出\_技术**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)枚举表明 VidPN 目标为 MIRACAST 设备。
-   QDC 的 Flags 参数值\_对[**QueryDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)的调用中的**所有\_路径**都不会返回连接到尚未附加活动监视器的 Miracast 目标的任何路径。
-   对于具有连接的 Miracast 监视器的每个路径， [**QueryDisplayConfig**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-querydisplayconfig)返回由 miracast 接收器报告的连接器类型。 内部 Miracast 接收器在[**DISPLAYCONFIG\_视频\_的技术**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)枚举\_输出中报告**DISPLAYCONFIG\_输出\_技术\_Miracast**的值。 例如，如果 Miracast 接收器报告电视已使用高清晰多媒体接口（HDMI）电缆连接到接收器，则**QueryDisplayConfig**会将目标类型报告为**DISPLAYCONFIG\_输出\_技术\_HDMI**。
-   [**DISPLAYCONFIG\_视频\_信号\_信息**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-displayconfig_video_signal_info)结构具有 VSync frequency 分隔成员**vSyncFreqDivider**，其使用方式类似于[**D3DKMDT\_视频\_信号\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)。**vSyncFreqDivider**。
-   [**DisplayConfigGetDeviceInfo**](https://docs.microsoft.com/windows/desktop/api/winuser/nf-winuser-displayconfiggetdeviceinfo)函数为任何目标提供基连接器类型。 对于 Miracast 目标，此函数始终返回值 " **DISPLAYCONFIG\_输出\_技术\_Miracast Miracast** [ **\_视频\_的" 视频**](https://docs.microsoft.com/windows/desktop/api/wingdi/ne-wingdi-displayconfig_video_output_technology)"。

 

 





