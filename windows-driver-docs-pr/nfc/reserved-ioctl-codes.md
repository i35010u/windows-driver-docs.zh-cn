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
ms.openlocfilehash: b8c17429afe64a4c7171363ebd757767182645f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566411"
---
# <a name="reserved-ioctl-codes"></a>保留的 IOCTL 代码


保留所有以下 IOCTL 代码，除非显式定义上方;该驱动程序必须返回状态\_无效\_设备\_从以下任一状态：

CTL\_代码 (文件\_设备\_NFP，0x0000， \*， \*) 通过 CTL\_代码 (文件\_设备\_NFP，0x00FF， \*， \*)

以下 Ioctl 可能用于 IHV 特有的功能：

CTL\_代码 (文件\_设备\_NFP，0x0100 \*， \*) 通过 CTL\_代码 (文件\_设备\_NFP，0x01FF， \*， \*)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[邻近 DDI 引用附近](https://msdn.microsoft.com/library/windows/hardware/jj866056)  
