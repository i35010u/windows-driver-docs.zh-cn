---
title: CM_PROB_DEVICE_NOT_THERE
description: CM_PROB_DEVICE_NOT_THERE
ms.assetid: 843afcc0-30ca-42f8-8c9b-3c4a56ec019d
keywords:
- CM_PROB_DEVICE_NOT_THERE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d8931b6fe5790b466fdc042956ec706425fffd
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279590"
---
# <a name="code-24---cm_prob_device_not_there"></a>代码 24-CM_PROB_DEVICE_NOT_THERE

此设备管理器错误消息表明设备似乎不存在。

## <a name="error-code"></a>错误代码

24

### <a name="display-message"></a>显示消息

"此设备不存在、未正常工作，或者没有安装其所有驱动程序。 （Code 24） "

### <a name="recommended-resolution"></a>建议的解决方法

问题可能是硬件损坏，或者可能需要新的驱动程序。 已准备删除的设备将处于此状态。 如果驱动程序的**DriverEntry**例程检测到设备，但**DriverEntry**例程稍后失败，则可以设置此错误代码。

**注意**  适用于 windows XP 和更高版本的 Windows， **DriverEntry**问题具有不同的错误代码。
