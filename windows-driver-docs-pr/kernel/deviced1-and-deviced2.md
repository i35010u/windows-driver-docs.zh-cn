---
title: DeviceD1 和 DeviceD2
description: DeviceD1 和 DeviceD2
ms.assetid: 88e9e1bf-c797-4e00-b540-1b2f8d48300a
keywords:
- DeviceD1
- DeviceD2
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d583fa7d4aab57f7c58a13dc64cffad5c98e32d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838742"
---
# <a name="deviced1-and-deviced2"></a>DeviceD1 和 DeviceD2





[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的**DeviceD1**和**DeviceD2**成员指示设备硬件是否支持这些设备电源状态。 每个都是单个位，在设备支持状态时设置，如果设备不支持此状态，则会将其清除。 操作系统假定所有设备都支持 D0 和 D3[设备电源状态](device-power-states.md)。

 

 




