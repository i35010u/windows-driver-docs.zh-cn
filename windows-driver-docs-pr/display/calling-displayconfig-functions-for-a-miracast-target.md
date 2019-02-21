---
title: 用于 Miracast 目标调用 DisplayConfig 函数
ms.assetid: D408986B-B33B-4A96-B93C-2A2F301E74AF
description: 用于 Miracast 目标调用 DisplayConfig 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 252ce447878a3d2742ee25954b90c33052f1c124
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546005"
---
# <a name="calling-displayconfig-functions-for-a-miracast-target"></a>用于 Miracast 目标调用 DisplayConfig 函数


若要减少到支持 Miracast 的新目标，公开的现有应用程序的兼容性问题[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)并[ **SetDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569533)函数实现具有应用，从而查找 Miracast 目标的方法：

-   值为**DISPLAYCONFIG\_输出\_技术\_MIRACAST**中[ **DISPLAYCONFIG\_视频\_输出\_技术**](https://msdn.microsoft.com/library/windows/hardware/ff554003)枚举指示 VidPN 目标为 Miracast 设备。
-   Flags 参数值的**QDC\_所有\_路径**对的调用中[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215)不会返回连接到支持 Miracast 的任何路径不具有附加的活动监视器的目标。
-   为已连接的 Miracast 监视器，每个路径[ **QueryDisplayConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff569215) Miracast 接收器返回报告的连接器类型。 内部 Miracast 接收器报告的值**DISPLAYCONFIG\_输出\_技术\_MIRACAST**中[ **DISPLAYCONFIG\_视频\_输出\_技术**](https://msdn.microsoft.com/library/windows/hardware/ff554003)枚举。 例如，如果 Miracast 接收器报告是否电视已连接到接收器使用高清晰度多媒体接口 (HDMI) 电缆，然后**QueryDisplayConfig**将报告作为目标类型**DISPLAYCONFIG\_输出\_技术\_HDMI**。
-   [ **DISPLAYCONFIG\_视频\_信号\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff554007)结构有一个垂直同步频率分隔符成员， **vSyncFreqDivider**，类似于使用[ **D3DKMDT\_视频\_信号\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff546625)。**vSyncFreqDivider**。
-   [ **DisplayConfigGetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff553903)函数提供的基本连接符类型的任何目标。 对于 Miracast 目标，此函数始终返回的值**DISPLAYCONFIG\_输出\_技术\_MIRACAST**中[ **DISPLAYCONFIG\_视频\_输出\_技术**](https://msdn.microsoft.com/library/windows/hardware/ff554003)枚举。

 

 





