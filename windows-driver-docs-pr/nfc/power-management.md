---
title: NFP 电源管理
description: NFP 电源管理
ms.assetid: A47F4B01-A912-410A-8CF8-656D2C125148
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43ec9d1d166be94a7cdadd58138adf33518a2e4d
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382953"
---
# <a name="nfp-power-management"></a>NFP 电源管理


NFP 设备在三种电源模式下运行。 这些模式包括 *活动*、 *空闲*、 *待机*和 *电源删除*。 当禁用了对设备的发布或订阅时，NFP 设备可以进入低功耗模式。 NFP 驱动程序会将设备转换为电源模式之一，以响应 Windows 中的启用或禁用通知。

NFP 驱动程序将接收 [**ioctl \_ nfp \_ ENABLE**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_enable) 或 [**ioctl \_ nfp \_ 禁用**](/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable) 控制代码，以启用或禁用订阅、发布和状态事件。 这些控制代码还会触发设备的电源模式更改。 [就近现场近程 (nfp) 用于连接备用平台的电源管理](/windows-hardware/design/device-experiences/near-field-promiximity--nfp--power-management-for-modern-standby-platforms)主题详细说明了 nfp 设备的电源模式更改。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)