---
title: 保留的 IOCTL 代码
ms.assetid: A2A67F8E-0A29-429E-935C-39368EFD9772
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: 有关 NFC 驱动程序的保留 ioctl 代码的信息，必须返回 STATUS_INVALID_DEVICE_STATE。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35b529f5b98e170abad35583a6fcf152cd130bf2
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381671"
---
# <a name="reserved-ioctl-codes"></a>保留的 IOCTL 代码


除非在上面明确定义，否则将保留以下所有 IOCTL 代码：驱动程序必须 \_ \_ 从以下任一项返回状态无效的设备 \_ 状态：

CTL \_ code (file \_ device \_ nfp，0x0000， \* ， \*) 到 ctl \_ Code (file \_ device \_ nfp，0x00FF， \* ， \*) 

以下 IOCTLs 可用于特定于 IHV 的功能：

CTL \_ code (file \_ device \_ nfp，0x0100， \* ， \*) 到 ctl \_ Code (file \_ device \_ nfp，0x01FF， \* ， \*) 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)