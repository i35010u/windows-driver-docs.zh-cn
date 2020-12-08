---
title: DeviceD1 和 DeviceD2
description: DeviceD1 和 DeviceD2
keywords:
- DeviceD1
- DeviceD2
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 184503a11376ca9568d1d2012442d18cdc4fa86a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792785"
---
# <a name="deviced1-and-deviced2"></a>DeviceD1 和 DeviceD2





[**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的 **DeviceD1** 和 **DeviceD2** 成员指示设备硬件是否支持这些设备电源状态。 每个都是单个位，在设备支持状态时设置，如果设备不支持此状态，则会将其清除。 操作系统假定所有设备都支持 D0 和 D3 [设备电源状态](device-power-states.md)。

 

