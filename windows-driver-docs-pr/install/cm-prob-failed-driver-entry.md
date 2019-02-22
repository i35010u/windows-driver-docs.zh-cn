---
title: CM_PROB_FAILED_DRIVER_ENTRY
description: CM_PROB_FAILED_DRIVER_ENTRY
ms.assetid: e1345892-69db-4135-be5b-1d182a2a1d66
keywords:
- CM_PROB_FAILED_DRIVER_ENTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c105dedf0bee0d2caf7e9ec929e96e7cb3db017e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547730"
---
# <a name="cmprobfaileddriverentry"></a>CM_PROB_FAILED_DRIVER_ENTRY

此函数保留供系统使用。
该驱动程序返回了失败从其**DriverEntry**例程。

## <a name="error-code"></a>错误代码

37

### <a name="display-message"></a>显示消息

"Windows 无法初始化这个硬件设备驱动程序。 （代码 37）"

### <a name="recommended-resolution"></a>建议的解决方法

重新安装或获取新的驱动程序。

**请注意**  如果**DriverEntry**例程将返回 STATUS_INSUFFICIENT_RESOURCES，设备管理器报告[CM_PROB_OUT_OF_MEMORY](cm-prob-out-of-memory.md)错误代码。
