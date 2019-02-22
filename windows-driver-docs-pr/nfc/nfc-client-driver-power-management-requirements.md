---
title: NFC 客户端驱动程序电源管理要求
ms.assetid: FBA0821B-859F-4A44-998E-E00162FBD265
keywords:
- NFC
- 附近通信
- 近程
- 邻近附近
- NFP
description: 有关会议上连接待机 NFP 设备的要求的信息。 平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a6d3968dbe771d7cdb638beddfbd7411b8f0e76
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556067"
---
# <a name="nfc-client-driver-power-management-requirements"></a>NFC 客户端驱动程序电源管理要求


NFC 客户端驱动程序必须实现 D0 和 D3 电源，如下所示处理回调，以符合已连接的备用平台上的 NFP 设备要求：

-   NFC 客户端驱动程序必须确保当驱动程序将从 D3-&gt; D0 它可以在不超过 100 毫秒之后恢复的状态。 这是为了确保 NFC 操作可能需要立即上切换屏幕的位置。

-   NFC 客户端驱动程序还必须确保功率消耗小于 1mW 处于 D3 状态时。 这是为了确保在关闭屏幕时没有显著的功率消耗。

为了满足这些目标，以下为建议的 NFC 客户端驱动程序：

-   可以通过转到 power 删除或硬断电满足这些要求的 NFC 控制器中，我们建议 NFC 客户端驱动程序将重新初始化期间 D0-的芯片组&gt;D3，然后从 D3-&gt; D0 转换。

-   NFC 控制器需要修补程序下载没有非易失性 (即，基于 RAM) 的情况下由于内存中，我们建议 NFC 客户端驱动程序启用和禁用期间 D0-待机模式&gt;D3 和 D3-&gt; D0 过渡，分别。 完整的初始化完成 (HostActionStart) 时从 D3Final-转&gt;D0 和未初始化 (HostActionStop) 完成时从 D0-&gt; D3Final。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[NFC 类扩展 (CX) 引用](https://msdn.microsoft.com/library/windows/hardware/dn905536)  
