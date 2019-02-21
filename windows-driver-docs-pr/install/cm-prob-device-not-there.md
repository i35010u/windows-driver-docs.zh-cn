---
title: CM_PROB_DEVICE_NOT_THERE
description: CM_PROB_DEVICE_NOT_THERE
ms.assetid: 843afcc0-30ca-42f8-8c9b-3c4a56ec019d
keywords:
- CM_PROB_DEVICE_NOT_THERE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ab4135b18bd4ac805c095df072297ee192d4ac9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524361"
---
# <a name="cmprobdevicenotthere"></a>CM_PROB_DEVICE_NOT_THERE

此函数保留供系统使用。

设备似乎存在。

## <a name="error-code"></a>错误代码

24

### <a name="display-message"></a>显示消息

"此设备不存在、 工作不正常，或者不包含所有安装其驱动程序。 （代码 24）"

### <a name="recommended-resolution"></a>建议的解决方法

该问题可能是损坏的硬件，或可能需要新的驱动程序。 设备处于此状态，如果已准备进行删除。 如果驱动程序，可以设置此错误代码**DriverEntry**例程检测到设备，但**DriverEntry**例程的更高版本失败。

**请注意**  适用于 Windows XP 和更高版本的 Windows， **DriverEntry**问题都有单独的错误代码。
