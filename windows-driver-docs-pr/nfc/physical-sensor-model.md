---
title: 物理传感器模型
description: 物理传感器模型
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7465da0fe40c85922dc9dc7987395de0587887b7
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091156"
---
# <a name="physical-sensor-model"></a>物理传感器模型


系统中的典型配置是具有一个实现 NFC 的 NFP 提供程序。 但是，在给定系统中可以有多个 NFP 提供程序，每个提供程序支持不同或相同的 NFP 技术。 例如，给定的 tablet 外形规格系统可能会在其边缘周围放置多个 NFC 天线，并且 tablet 的背面可能有一个用于连接到无线坞的附加的 NFC/TransferJet 触摸点。 在此示例系统上，NFP 的物理建模中，不会在单个提供程序中单独寻址这些额外的天线。 为了提供可单独寻址的 touchpoints，系统 maker 需要为每个天线和 NFP 技术实现特定的 NFP 提供程序实例。 当任何设备在其中一个提供程序近程时，已发布的消息将传输到所有订阅服务器。

 

 
## <a name="related-topics"></a>相关主题
[近现场通信 (NFC) API 参考](/windows-hardware/drivers/ddi/_nfpdrivers/)
