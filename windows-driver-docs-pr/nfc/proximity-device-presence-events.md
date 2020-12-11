---
title: 邻近感应设备存在事件
description: 邻近感应设备存在事件
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5cab0b11af0b14a01bd86a21992c5d0cb6164167
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090836"
---
# <a name="proximity-device-presence-events"></a>邻近感应设备存在事件


NFP 提供程序使客户端能够在近程设备在触发操作) 的窗口 (检测到或离职时接收事件。 每当 NFP 提供程序检测到邻近性时，这意味着提供程序当前可以与一个或多个近程设备通信，提供程序需要发出 *DeviceArrived* 事件。 当 NFP 提供程序无法再与任何近程设备通信时，它需要发出 *DeviceDeparted* 事件。

NFP 提供程序还需要跟踪近程设备的状态，以便正确确保已发布的消息仅在设备处于邻近状态时传输一次。 这些事件应基于相同的指标。 对于能够同时与多个近程设备通信的 NFP 提供程序，状态事件应该是所有存在性的聚合。 如果提供程序在近程设备上同时支持0到 N，则只会在从0到1的转换和1到0的当前近程设备之间传输事件。 请注意，NFC 不支持此功能。

 

 
## <a name="related-topics"></a>相关主题
[近现场通信 (NFC) API 参考](/windows-hardware/drivers/ddi/_nfpdrivers/)
