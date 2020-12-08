---
title: D1Latency、D2Latency 和 D3Latency
description: D1Latency、D2Latency 和 D3Latency
keywords:
- D1Latency
- D2Latency
- D3Latency
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a749f11fbf71e73a6b710edde111fc1ee2a416e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792819"
---
# <a name="d1latency-d2latency-and-d3latency"></a>D1Latency、D2Latency 和 D3Latency





[**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的 **D1Latency**、 **D2Latency** 和 **D3Latency** 成员包含设备需要从每个休眠状态返回到 D0 状态的大概时间（以100微秒为单位）。 对于不支持的任何设备电源状态，驱动程序应为其指定延迟时间为零。

 

