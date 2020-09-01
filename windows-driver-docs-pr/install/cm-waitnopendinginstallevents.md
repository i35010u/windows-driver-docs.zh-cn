---
title: CM_WaitNoPendingInstallEvents
description: CM_WaitNoPendingInstallEvents
ms.assetid: b9922576-9e7e-454f-88e0-948a1e16523f
keywords:
- CM_WaitNoPendingInstallEvents 设备和驱动程序安装
topic_type:
- apiref
api_name:
- CM_WaitNoPendingInstallEvents
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f59d0f53ccb049d816bbf539b8015843090f1f41
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097399"
---
# <a name="cm_waitnopendinginstallevents"></a>CM_WaitNoPendingInstallEvents

此函数保留供系统使用。

**CM_WaitNoPendingInstallEvents** 在 *Cfgmgr32* 中定义，如下所示：

```c
#define CM_WaitNoPendingInstallEvents CMP_WaitNoPendingInstallEvents
```

换句话说， **CM_WaitNoPendingInstallEvents** 只是 [**CMP_WaitNoPendingInstallEvents**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_waitnopendinginstallevents)的另一个名称。 由于没有名为 **CM_WaitNoPendingInstallEvents**的实际函数，因此 **GetProcAddress** 将返回 **NULL**。