---
title: NFC 客户端驱动程序电源管理要求
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: 有关在连接待机时满足 NFP 设备的要求的信息。 platforms
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11854c775f91b77b9ff24c516644164ce061ef49
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813521"
---
# <a name="nfc-client-driver-power-management-requirements"></a>NFC 客户端驱动程序电源管理要求


NFC 客户端驱动程序必须实现 D0 和 D3 电源处理回调，以便满足连接备用平台上的 NFP 设备的要求：

-   NFC 客户端驱动程序必须确保驱动程序从 D3- &gt; D0 状态（它可在100ms 中恢复）。 这是为了确保可以在切换屏幕时立即进行 NFC 操作。

-   当处于 D3 状态时，NFC 客户端驱动程序还必须确保功率消耗小于1mW。 这是为了确保在屏幕关闭时不会有明显的功率消耗。

为了满足这些目标，推荐使用以下 NFC 客户端驱动程序：

-   对于可以通过关机或硬关机来满足这些要求的 NFC 控制器，我们建议 NFC 客户端驱动程序在 D0-D3 期间重新初始化芯片组 &gt; ，然后再从 D3- &gt; D0 转换。

-   对于需要修补程序 (下载的 NFC 控制器（即基于 RAM 的) 内存），我们建议在 D0- &gt; D3 和 d3 d0 转换期间使用 nfc 客户端驱动程序启用和禁用备用模式 &gt; 。 从 D3Final &gt; 和 deinitialization () HostActionStop 从 d0-D3Final 开始时，将执行完全初始化 (HostActionStart) &gt; 。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/index)
