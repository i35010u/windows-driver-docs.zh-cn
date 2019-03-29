---
title: 在检测期间验证 HwScsiFindAdapter 中的资源范围
description: 在检测期间验证 HwScsiFindAdapter 中的资源范围
ms.assetid: 2909aac2-714e-4353-8006-06cf68e4dfc8
keywords:
- SCSI 微型端口驱动程序 WDK 存储，即插即用
- 即插即用 WDK SCSI
- Plug and Play WDK SCSI
- 转换 SCSI 微型端口驱动程序
- 资源范围 WDK SCSI
- HwScsiFindAdapter
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c1525edd5204f78dee4eb2b4cb8f6d0f2e24da8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568421"
---
# <a name="verify-resource-ranges-in-hwscsifindadapter-during-detection"></a>在检测期间验证 HwScsiFindAdapter 中的资源范围


## <span id="ddk_verify_resource_ranges_in_hwscsifindadapter_during_detection_kg"></span><span id="DDK_VERIFY_RESOURCE_RANGES_IN_HWSCSIFINDADAPTER_DURING_DETECTION_KG"></span>


虽然设备驱动程序的检测是插下通常不必要的但端口驱动程序可能会在调用插微型端口驱动程序的[ *HwScsiFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff557300)例程，以检测设备上nonenumerable 总线。 尽管此操作类似于 Microsoft Windows NT 4.0 中的检测，但微型端口驱动程序必须注意不要在可能正由另一台设备使用的范围上执行。

微型端口驱动程序应调用[ **ScsiPortValidateRange** ](https://msdn.microsoft.com/library/windows/hardware/ff564761)之前调用[ **ScsiPortGetDeviceBase** ](https://msdn.microsoft.com/library/windows/hardware/ff564629)以确保微型端口驱动程序所提供的范围是安全地使用。 微型端口驱动程序必须做好**ScsiPortGetDeviceBase**失败并返回**NULL**指针。 微型端口驱动程序还应避免映射内存开始地址为零，这使我们无法检测的故障**ScsiPortGetDeviceBase**某些系统上。

 

 




