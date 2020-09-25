---
title: CM_PROB_FAILED_START
description: CM_PROB_FAILED_START
ms.assetid: a7759bcd-1806-4d7a-8ff0-3b03abcae08b
keywords:
- CM_PROB_FAILED_START
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 39b9c7d450fa28bc3655b1332f15a90280a983f3
ms.sourcegitcommit: 29c2e6dd8a3de3c11822d990adf1edd774f8a136
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91230047"
---
# <a name="code-10---cm_prob_failed_start"></a>代码 10 - CM_PROB_FAILED_START

此设备管理器错误消息指示设备无法启动。

## <a name="error-code"></a>错误代码

10

### <a name="display-message"></a>显示消息

如果设备的 [硬件密钥](opening-a-device-s-hardware-key.md) 包含 "FailReasonString" 值，则会将值字符串显示为错误消息。  (驱动程序或枚举器提供此注册表字符串值。如果硬件密钥不包含 "FailReasonString" 值，则 ) ，将显示以下一般错误消息：

"此设备无法启动。  (代码 10) "

"尝试升级此设备的设备驱动程序。"

### <a name="recommended-resolution"></a>推荐的解决方案

选择 " **更新驱动程序**"，这将启动硬件更新向导。

当设备的驱动程序堆栈中的某个驱动程序 IRP_MN_START_DEVICE 失败时，将设置此错误代码。 如果堆栈中存在多个驱动程序，则很难确定失败的驱动程序。

请参阅设备上的 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md) 属性，了解为 [启动 IRP](../kernel/irp-mn-start-device.md)返回的失败代码。

有关其他信息，请参阅 [检索设备实例的状态和问题代码](retrieving-the-status-and-problem-code-for-a-device-instance.md)。

## <a name="for-driver-developers"></a>面向驱动程序开发人员

设备堆栈中的某个驱动程序未能 [启动 IRP](../kernel/irp-mn-start-device.md)。 设备上的 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md) 属性应指示故障代码。

如果设备驱动程序堆栈中的某个驱动程序是 UMDF 驱动程序，并且该设备上的 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md) 属性是 STATUS_DRIVER_PROCESS_TERMINATED 的，则此信息可能对驱动程序的所有者有帮助，以诊断问题：
* [确定反射器终止主机进程的原因](../wdf/determining-why-the-reflector-terminated-the-host-process.md)
* [排查 UMDF 2.0 驱动程序崩溃问题](../wdf/debugging-umdf-2-0-drivers.md)

