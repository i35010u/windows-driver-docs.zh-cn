---
title: D1Latency、D2Latency 和 D3Latency
description: D1Latency、D2Latency 和 D3Latency
ms.assetid: 6ad72b77-ec36-461c-8f4f-030d67e5a135
keywords:
- D1Latency
- D2Latency
- D3Latency
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ac1c4d4119dee737ce4e5261a5b9685f8a7844d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191969"
---
# <a name="d1latency-d2latency-and-d3latency"></a>D1Latency、D2Latency 和 D3Latency





[**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的**D1Latency**、 **D2Latency**和**D3Latency**成员包含设备需要从每个休眠状态返回到 D0 状态的大概时间（以100微秒为单位）。 对于不支持的任何设备电源状态，驱动程序应为其指定延迟时间为零。

 

