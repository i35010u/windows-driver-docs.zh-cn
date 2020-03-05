---
title: CM_PROB_FAILED_DRIVER_ENTRY
description: CM_PROB_FAILED_DRIVER_ENTRY
ms.assetid: e1345892-69db-4135-be5b-1d182a2a1d66
keywords:
- CM_PROB_FAILED_DRIVER_ENTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40198115ad0c807836b3fb33c7d142923144bdd6
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279568"
---
# <a name="code-37---cm_prob_failed_driver_entry"></a>代码 37-CM_PROB_FAILED_DRIVER_ENTRY

此设备管理器错误消息指示驱动程序从其**DriverEntry**例程返回了故障。

## <a name="error-code"></a>错误代码

37

### <a name="display-message"></a>显示消息

"Windows 无法初始化此硬件的设备驱动程序。 （代码37） "

### <a name="recommended-resolution"></a>建议的解决方法

重新安装或获取新驱动程序。

**请注意**  如果**DriverEntry**例程返回 STATUS_INSUFFICIENT_RESOURCES，设备管理器将报告[CM_PROB_OUT_OF_MEMORY](cm-prob-out-of-memory.md)错误代码。
