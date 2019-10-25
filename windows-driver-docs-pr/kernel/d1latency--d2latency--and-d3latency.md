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
ms.openlocfilehash: eed503600bb9ea9ad4e4a47160c47e588a04e6bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836970"
---
# <a name="d1latency-d2latency-and-d3latency"></a>D1Latency、D2Latency 和 D3Latency





[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的**D1Latency**、 **D2Latency**和**D3Latency**成员包含设备需要从每个休眠状态返回到 D0 状态的大概时间（以100微秒为单位）。 对于不支持的任何设备电源状态，驱动程序应为其指定延迟时间为零。

 

 




