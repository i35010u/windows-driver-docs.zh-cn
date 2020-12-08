---
title: CM_PROB_DEVICE_NOT_THERE
description: CM_PROB_DEVICE_NOT_THERE
keywords:
- CM_PROB_DEVICE_NOT_THERE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27c115d8f220d588b95eed2c12680084fd470c96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814309"
---
# <a name="code-24---cm_prob_device_not_there"></a>代码 24 - CM_PROB_DEVICE_NOT_THERE

此设备管理器错误消息表明设备似乎不存在。

## <a name="error-code"></a>错误代码

24

### <a name="display-message"></a>显示消息

"此设备不存在、未正常工作，或者没有安装其所有驱动程序。  (代码 24) "

### <a name="recommended-resolution"></a>推荐的解决方案

问题可能是硬件损坏，或者可能需要新的驱动程序。 已准备删除的设备将处于此状态。 如果驱动程序的 **DriverEntry** 例程检测到设备，但 **DriverEntry** 例程稍后失败，则可以设置此错误代码。

**注意**  对于 Windows XP 和更高版本的 Windows， **DriverEntry** 问题具有单独的错误代码。
