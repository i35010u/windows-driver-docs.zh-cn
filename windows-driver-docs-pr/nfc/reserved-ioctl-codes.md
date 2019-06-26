---
title: 保留的 IOCTL 代码
ms.assetid: A2A67F8E-0A29-429E-935C-39368EFD9772
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: NFC 驱动程序，它必须返回 STATUS_INVALID_DEVICE_STATE 保留的 ioctl 代码的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 226a61dd529991313a5415e7397111d75c0466b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386512"
---
# <a name="reserved-ioctl-codes"></a>保留的 IOCTL 代码


保留所有以下 IOCTL 代码，除非显式定义上方;该驱动程序必须返回状态\_无效\_设备\_从以下任一状态：

CTL\_代码 (文件\_设备\_NFP，0x0000， \*， \*) 通过 CTL\_代码 (文件\_设备\_NFP，0x00FF， \*， \*)

以下 Ioctl 可能用于 IHV 特有的功能：

CTL\_代码 (文件\_设备\_NFP，0x0100 \*， \*) 通过 CTL\_代码 (文件\_设备\_NFP，0x01FF， \*， \*)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
