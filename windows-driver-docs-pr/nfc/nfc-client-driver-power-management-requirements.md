---
title: NFC 客户端驱动程序电源管理要求
ms.assetid: FBA0821B-859F-4A44-998E-E00162FBD265
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
description: 有关在连接待机时满足 NFP 设备的要求的信息。 适用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d31fa09026ad5444575987d22acfe5a15039ae6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831872"
---
# <a name="nfc-client-driver-power-management-requirements"></a>NFC 客户端驱动程序电源管理要求


NFC 客户端驱动程序必须实现 D0 和 D3 电源处理回调，以便满足连接备用平台上的 NFP 设备的要求：

-   NFC 客户端驱动程序必须确保驱动程序从 D3&gt; D0 状态（它可在小于100ms 的情况恢复）。 这是为了确保可以在切换屏幕时立即进行 NFC 操作。

-   当处于 D3 状态时，NFC 客户端驱动程序还必须确保功率消耗小于1mW。 这是为了确保在屏幕关闭时不会有明显的功率消耗。

为了满足这些目标，推荐使用以下 NFC 客户端驱动程序：

-   对于可以通过电源删除或硬关机来满足这些要求的 NFC 控制器，我们建议 NFC 客户端驱动程序在 D0&gt; D3 期间重新初始化芯片组，然后从 D3&gt; D0 转换。

-   对于需要修补程序下载的 NFC 控制器（即基于 RAM 的内存），我们建议在 D0&gt; D3 和 D3&gt; D0 转换期间使用 NFC 客户端驱动程序启用和禁用备用模式。 从 D3Final-&gt; D0 进行完全初始化（HostActionStart）后，从 D0&gt; D3Final 开始时，将执行完全初始化。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[NFC 类扩展（CX）参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
