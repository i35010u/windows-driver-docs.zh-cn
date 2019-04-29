---
title: CM_PROB_FAILED_START
description: CM_PROB_FAILED_START
ms.assetid: a7759bcd-1806-4d7a-8ff0-3b03abcae08b
keywords:
- CM_PROB_FAILED_START
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 957882d0ee0ae0e60c03742becd233ea83baf2a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391482"
---
# <a name="cmprobfailedstart"></a>CM_PROB_FAILED_START

此函数保留供系统使用。

设备启动失败。

## <a name="error-code"></a>错误代码

10

### <a name="display-message"></a>显示消息

如果设备的硬件密钥包含"FailReasonString"值，值字符串将显示为错误消息。 （驱动程序或枚举器提供了此注册表字符串值。）如果硬件密钥不包含"FailReasonString"值，显示以下一般性错误消息：

"此设备无法启动。 （代码 10）"

"请尝试升级此设备的设备驱动程序"。

### <a name="recommended-resolution"></a>建议的解决方法

选择**更新驱动程序**，这将启动硬件更新向导。

当设备的驱动程序堆栈中的驱动程序出现故障时执行了 IRP_MN_START_DEVICE 设置此错误代码。 如果堆栈中有许多驱动程序，它可能很难确定的失败。
