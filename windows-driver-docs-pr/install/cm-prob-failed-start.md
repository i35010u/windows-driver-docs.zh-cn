---
title: CM_PROB_FAILED_START
description: CM_PROB_FAILED_START
ms.assetid: a7759bcd-1806-4d7a-8ff0-3b03abcae08b
keywords:
- CM_PROB_FAILED_START
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6098582a3ff386db61c4f6d92dd25925f98cae86
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097345"
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