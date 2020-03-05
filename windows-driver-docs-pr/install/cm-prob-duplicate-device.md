---
title: CM_PROB_DUPLICATE_DEVICE
description: CM_PROB_DUPLICATE_DEVICE
ms.assetid: db0f6c98-d314-4882-ac8e-c73254f41c98
keywords:
- CM_PROB_DUPLICATE_DEVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7fe56dae488b031510d515b0c3754b456cb7335
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279576"
---
# <a name="code-42---cm_prob_duplicate_device"></a>代码 42-CM_PROB_DUPLICATE_DEVICE

此设备管理器错误消息指示检测到重复的设备。

## <a name="error-code"></a>错误代码

42

### <a name="display-message"></a>显示消息

"Windows 无法加载该硬件的设备驱动程序，因为系统中已有一个重复的设备正在运行。 （代码42） "

### <a name="recommended-resolution"></a>建议的解决方法

发生以下情况之一时，会报告此错误：

- 在操作系统检测到设备从旧位置丢失之前，将在计算机的新位置发现具有序列号的设备。 这通常发生在将设备移动到另一个位置（无论是快速还是在计算机处于待机或休眠状态时）。

    在这种情况下，您可以通过重新启动计算机来解决该问题。

- 总线驱动程序错误地在总线上创建两个名称相同的子节点。 这是因为总线上的多个设备报告相同的序列号。 这也可能是由于总线驱动程序错误地报告了两个或多个设备的相同硬件标识符导致的。

    在这种情况下，你应该与[Microsoft 支持](https://support.microsoft.com/en-us)部门联系，以获取有关此问题的更多帮助。
