---
title: NFC 电源管理
description: NFC 电源管理
ms.assetid: 7B45730F-A49D-45E0-B314-0464141E3C8B
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62c6ecb45aae3e8d1c0c8515ede443c60b86c7b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383552"
---
# <a name="nfc-power-management"></a>NFC 电源管理


NFC 驱动程序应以智能方式管理设备的电源状态。 以下是 Ihv 提供 NFC 驱动程序的一般准则。

**邻近电源管理。** 如果有任何活动邻近发布、 订阅或智能卡 present/不存在操作挂起，或如果禁用了邻近无线电的状态，然后 NFC 驱动程序可能会停用的发现/轮询循环的 P2P 和标记发现部分。

**安全元素电源管理。** 如果没有安全元素都公开给读者全面了解仿真，或如果禁用安全元素单选状态，然后 NFC 驱动程序可能会停用卡仿真的循环部分的发现/轮询。

**总体电源管理。** 如果邻近和卡仿真操作处于非活动状态，然后 NFC 驱动程序可能会切断电源设备完全通过转换为低功耗状态 （D3 状态） （当系统处于 S0 状态） 时使用空闲的电源管理。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  


