---
title: 保留的 IOCTL 代码
ms.assetid: A2A67F8E-0A29-429E-935C-39368EFD9772
keywords:
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
description: 有关 NFC 驱动程序的保留 ioctl 代码的信息，必须返回 STATUS_INVALID_DEVICE_STATE。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c57e740f24ffc479e5388398145dc6da4f28d800
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834026"
---
# <a name="reserved-ioctl-codes"></a>保留的 IOCTL 代码


除非在上面明确定义，否则将保留以下所有 IOCTL 代码：驱动程序必须返回状态\_\_设备的状态无效，\_状态如下：

CTL\_代码（FILE\_DEVICE\_NFP，0x0000，\*，\*）到 CTL\_CODE （FILE\_DEVICE\_NFP，0x00FF，\*，\*）

以下 IOCTLs 可用于特定于 IHV 的功能：

CTL\_代码（FILE\_DEVICE\_NFP，0x0100，\*，\*）到 CTL\_CODE （FILE\_DEVICE\_NFP，0x01FF，\*，\*）

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近字段邻近 DDI 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
