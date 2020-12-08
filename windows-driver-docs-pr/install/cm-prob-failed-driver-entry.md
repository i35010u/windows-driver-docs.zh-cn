---
title: CM_PROB_FAILED_DRIVER_ENTRY
description: CM_PROB_FAILED_DRIVER_ENTRY
keywords:
- CM_PROB_FAILED_DRIVER_ENTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5e3fc76e6cb1098daa28af714cd362d9dea33da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783155"
---
# <a name="code-37---cm_prob_failed_driver_entry"></a>代码 37 - CM_PROB_FAILED_DRIVER_ENTRY

此设备管理器错误消息指示驱动程序从其 **DriverEntry** 例程返回了故障。

## <a name="error-code"></a>错误代码

37

### <a name="display-message"></a>显示消息

"Windows 无法初始化此硬件的设备驱动程序。  (代码 37) "

### <a name="recommended-resolution"></a>推荐的解决方案

重新安装或获取新驱动程序。

**注意**  如果 **DriverEntry** 例程返回 STATUS_INSUFFICIENT_RESOURCES，设备管理器会报告 [CM_PROB_OUT_OF_MEMORY](cm-prob-out-of-memory.md) 错误代码。
