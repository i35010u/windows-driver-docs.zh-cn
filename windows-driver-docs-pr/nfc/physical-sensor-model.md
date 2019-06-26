---
title: 物理传感器模型
description: 物理传感器模型
ms.assetid: D3887E09-E0A4-4FBC-9D26-344016047235
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11ad14402cee7f7d867c3544df56ff9926d71cd9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386532"
---
# <a name="physical-sensor-model"></a>物理传感器模型


在系统中的典型配置是具有一个 NFP 提供程序实现 NFC。 但是，可以有多个 NFP 提供程序在给定系统上，每个支持不同或相同 NFP 技术。 例如，给定的平板电脑外形规格系统可能有多个放置其边缘周围的 NFC 天线和状态的平板电脑可能有一个其他组合的 NFC/TransferJet 触摸点用来连接到的无线停靠。 在此示例系统上 NFP 物理建模，这些其他的天线不是单个提供程序中单独寻址。 若要提供单独寻址的接触点，系统创建者需要为每个天线和 NFP 技术实现特定的 NFP 提供程序实例。 当任何设备变为近程跨这些提供程序之一时，已发布的消息传输到所有订阅服务器。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

