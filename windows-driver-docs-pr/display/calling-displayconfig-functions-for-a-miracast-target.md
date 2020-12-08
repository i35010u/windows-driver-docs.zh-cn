---
title: 对 Miracast 目标调用 DisplayConfig 函数
description: 对 Miracast 目标调用 DisplayConfig 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31fd4640a3612de642d6dedd2b3cbaf0cdcbfd30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810397"
---
# <a name="calling-displayconfig-functions-for-a-miracast-target"></a>对 Miracast 目标调用 DisplayConfig 函数


为了降低公开给新 Miracast 目标的现有应用的兼容性问题， [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) 和 [**SetDisplayConfig**](/windows/win32/api/winuser/nf-winuser-setdisplayconfig) 函数实现有多种方法可让应用查找 Miracast 目标：

-   [**DISPLAYCONFIG \_ 视频 \_ 输出 \_ 技术**](/windows/win32/api/wingdi/ne-wingdi-displayconfig_video_output_technology)枚举中的 **DISPLAYCONFIG \_ OUTPUT \_ 技术 \_ MIRACAST** 值表明 VidPN 目标是 MIRACAST 设备。
-   在对 [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig)的调用中，QDC 的 Flags 参数值不会返回任何连接到尚未附加活动监视器的 Miracast 目标的路径 **\_ \_** 。
-   对于具有连接的 Miracast 监视器的每个路径， [**QueryDisplayConfig**](/windows/win32/api/winuser/nf-winuser-querydisplayconfig) 返回由 miracast 接收器报告的连接器类型。 内部 Miracast 接收器在 [**DISPLAYCONFIG \_ 视频 \_ 输出 \_ 技术**](/windows/win32/api/wingdi/ne-wingdi-displayconfig_video_output_technology)枚举中报告 **DISPLAYCONFIG \_ 输出 \_ 技术 \_ Miracast** 的值。 例如，如果 Miracast 接收器报告电视使用 High-Definition 多媒体接口 (HDMI) 电缆连接到接收器，则 **QueryDisplayConfig** 会将目标类型报告为 **DISPLAYCONFIG \_ 输出 \_ 技术 \_ HDMI**。
-   [**DISPLAYCONFIG \_ 视频 \_ 信号 \_ 信息**](/windows/win32/api/wingdi/ns-wingdi-displayconfig_video_signal_info)结构具有 VSync frequency 分隔成员 **vSyncFreqDivider**，其使用方式类似于 [**D3DKMDT \_ 视频 \_ 信号 \_ 信息**](/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_signal_info)。**vSyncFreqDivider**。
-   [**DisplayConfigGetDeviceInfo**](/windows/win32/api/winuser/nf-winuser-displayconfiggetdeviceinfo)函数为任何目标提供基连接器类型。 对于 Miracast 目标，此函数始终在 [**DISPLAYCONFIG \_ 视频 \_ 输出 \_ 技术**](/windows/win32/api/wingdi/ne-wingdi-displayconfig_video_output_technology)枚举中返回值 **DISPLAYCONFIG \_ OUTPUT \_ 技术 \_ Miracast** 。

 

