---
title: NFC 电源管理
description: NFC 电源管理
ms.assetid: 7B45730F-A49D-45E0-B314-0464141E3C8B
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdfac29b49b9c670bfa77128c79196382c48cbf4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842269"
---
# <a name="nfc-power-management"></a>NFC 电源管理


NFC 驱动程序应智能地管理设备的电源状态。 以下是提供 NFC 驱动程序的 Ihv 的一般准则。

**邻近电源管理。** 如果没有活动的邻近发布、订阅或智能卡存在或未完成的操作挂起，或者如果已禁用邻近无线电状态，则 NFC 驱动程序可能会停用发现/轮询循环的 P2P 和标记发现部分。

**保护元素电源管理。** 如果没有通过仿真向读取者公开安全的元素，或者如果禁用了安全元素无线电状态，则 NFC 驱动程序可以停用发现/轮询循环的卡仿真部分。

**整体电源管理。** 如果近程和卡仿真操作都已停用，则 NFC 驱动程序可以通过使用空闲电源管理（当系统处于 S0 状态时）转换为低功率状态（D3 状态）来完全关闭设备。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  


