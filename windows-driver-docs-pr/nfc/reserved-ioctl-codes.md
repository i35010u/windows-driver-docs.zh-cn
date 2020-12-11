---
title: 保留的 IOCTL 代码
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: 有关 NFC 驱动程序的保留 ioctl 代码的信息，必须返回 STATUS_INVALID_DEVICE_STATE。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0b1e998e65eea6c7b0bf0c3a1442582e5f61423
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091180"
---
# <a name="reserved-ioctl-codes"></a>保留的 IOCTL 代码


除非在上面明确定义，否则将保留以下所有 IOCTL 代码：驱动程序必须 \_ \_ 从以下任一项返回状态无效的设备 \_ 状态：

CTL \_ code (file \_ device \_ nfp，0x0000， \* ， \*) 到 ctl \_ Code (file \_ device \_ nfp，0x00FF， \* ， \*) 

以下 IOCTLs 可用于特定于 IHV 的功能：

CTL \_ code (file \_ device \_ nfp，0x0100， \* ， \*) 到 ctl \_ Code (file \_ device \_ nfp，0x01FF， \* ， \*) 

 

 
## <a name="related-topics"></a>相关主题
[近现场通信 (NFC) API 参考](/windows-hardware/drivers/ddi/_nfpdrivers/)
