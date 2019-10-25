---
title: 物理传感器模型
description: 物理传感器模型
ms.assetid: D3887E09-E0A4-4FBC-9D26-344016047235
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9808776e342698949d587a4093c4f62f451bbb0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831548"
---
# <a name="physical-sensor-model"></a>物理传感器模型


系统中的典型配置是具有一个实现 NFC 的 NFP 提供程序。 但是，在给定系统中可以有多个 NFP 提供程序，每个提供程序支持不同或相同的 NFP 技术。 例如，给定的 tablet 外形规格系统可能会在其边缘周围放置多个 NFC 天线，并且 tablet 的背面可能有一个用于连接到无线坞的附加的 NFC/TransferJet 触摸点。 在此示例系统上，NFP 的物理建模中，不会在单个提供程序中单独寻址这些额外的天线。 为了提供可单独寻址的 touchpoints，系统 maker 需要为每个天线和 NFP 技术实现特定的 NFP 提供程序实例。 当任何设备在其中一个提供程序近程时，已发布的消息将传输到所有订阅服务器。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

