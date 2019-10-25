---
title: NFP 电源管理
description: NFP 电源管理
ms.assetid: A47F4B01-A912-410A-8CF8-656D2C125148
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f420cb0b1d259a46e4181b0c853caad1170dd5ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834042"
---
# <a name="nfp-power-management"></a>NFP 电源管理


NFP 设备在三种电源模式下运行。 这些模式包括*活动*、*空闲*、*待机*和*电源删除*。 当禁用了对设备的发布或订阅时，NFP 设备可以进入低功耗模式。 NFP 驱动程序会将设备转换为电源模式之一，以响应 Windows 中的启用或禁用通知。

NFP 驱动程序将接收[**ioctl\_nfp\_启用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_enable)或[**ioctl\_nfp\_禁用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable)控制代码，以启用或禁用订阅、发布和状态事件。 这些控制代码还会触发设备的电源模式更改。 [邻近感应（NFP）用于连接备用平台的电源管理](https://docs.microsoft.com/windows-hardware/design/device-experiences/near-field-promiximity--nfp--power-management-for-modern-standby-platforms)主题提供了针对 NFP 设备的电源模式更改的详细说明。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

