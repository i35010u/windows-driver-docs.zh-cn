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
ms.openlocfilehash: 9f0dcc88c054b49988314d11c8609c3a333eed50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812717"
---
# <a name="reserved-ioctl-codes"></a>保留的 IOCTL 代码


除非在上面明确定义，否则将保留以下所有 IOCTL 代码：驱动程序必须 \_ \_ 从以下任一项返回状态无效的设备 \_ 状态：

CTL \_ code (file \_ device \_ nfp，0x0000， \* ， \*) 到 ctl \_ Code (file \_ device \_ nfp，0x00FF， \* ， \*) 

以下 IOCTLs 可用于特定于 IHV 的功能：

CTL \_ code (file \_ device \_ nfp，0x0100， \* ， \*) 到 ctl \_ Code (file \_ device \_ nfp，0x01FF， \* ， \*) 

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](/windows-hardware/drivers/ddi/index)
