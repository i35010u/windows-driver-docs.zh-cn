---
title: DeviceD1 和 DeviceD2
description: DeviceD1 和 DeviceD2
ms.assetid: 88e9e1bf-c797-4e00-b540-1b2f8d48300a
keywords:
- DeviceD1
- DeviceD2
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29deb70deedb0c6d6c67fbea1e6b358788cf7eef
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184763"
---
# <a name="deviced1-and-deviced2"></a>DeviceD1 和 DeviceD2





[**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)的**DeviceD1**和**DeviceD2**成员指示设备硬件是否支持这些设备电源状态。 每个都是单个位，在设备支持状态时设置，如果设备不支持此状态，则会将其清除。 操作系统假定所有设备都支持 D0 和 D3 [设备电源状态](device-power-states.md)。

 

