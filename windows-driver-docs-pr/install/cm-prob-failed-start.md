---
title: CM_PROB_FAILED_START
description: CM_PROB_FAILED_START
ms.assetid: a7759bcd-1806-4d7a-8ff0-3b03abcae08b
keywords:
- CM_PROB_FAILED_START
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 185621f49368d5e2ad85e3daf1531c3459a4ea4b
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558419"
---
# <a name="cm_prob_failed_start"></a>CM_PROB_FAILED_START

此函数保留供系统使用。

该设备启动失败。

## <a name="error-code"></a>错误代码

10

### <a name="display-message"></a>显示消息

如果设备的硬件密钥包含 "FailReasonString" 值，则会将值字符串显示为错误消息。 （驱动程序或枚举器提供此注册表字符串值。）如果硬件密钥不包含 "FailReasonString" 值，则会显示以下一般错误消息：

"此设备无法启动。 （代码10） "

"尝试升级此设备的设备驱动程序。"

### <a name="recommended-resolution"></a>建议的解决方法

选择 "**更新驱动程序**"，这将启动硬件更新向导。

当设备的驱动程序堆栈中的某个驱动程序 IRP_MN_START_DEVICE 失败时，将设置此错误代码。 如果堆栈中存在多个驱动程序，则很难确定失败的驱动程序。

请参阅设备上的[**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)属性，了解为启动 IRP 返回的失败代码。

有关其他信息，请参阅[检索设备实例的状态和问题代码](retrieving-the-status-and-problem-code-for-a-device-instance.md)。
