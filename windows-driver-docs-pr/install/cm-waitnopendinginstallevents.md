---
title: CM_WaitNoPendingInstallEvents
description: CM_WaitNoPendingInstallEvents
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
ms.openlocfilehash: cc887130ab65632b9d34c1fd6eab05d8383987e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783005"
---
# <a name="cm_waitnopendinginstallevents"></a>CM_WaitNoPendingInstallEvents

此函数保留供系统使用。

**CM_WaitNoPendingInstallEvents** 在 *Cfgmgr32* 中定义，如下所示：

```c
#define CM_WaitNoPendingInstallEvents CMP_WaitNoPendingInstallEvents
```

换句话说， **CM_WaitNoPendingInstallEvents** 只是 [**CMP_WaitNoPendingInstallEvents**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_waitnopendinginstallevents)的另一个名称。 由于没有名为 **CM_WaitNoPendingInstallEvents** 的实际函数，因此 **GetProcAddress** 将返回 **NULL**。
