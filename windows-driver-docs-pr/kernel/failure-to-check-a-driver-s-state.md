---
title: 无法检查驱动程序的状态
description: 无法检查驱动程序的状态
ms.assetid: 963f79f6-2282-41bd-9cf4-bd5bc02a510e
keywords:
- 可靠性 WDK 内核，驱动程序状态检查
- 检查驱动程序状态
- 驱动程序状态检查
- 验证驱动程序状态
- 正确的设备状态 WDK 内核
- 设备状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2f67b5b97a2eae9fdba1545fd1c6586cc25b8c6
ms.sourcegitcommit: 01bcf26722f1a51d2b5ebcdcbc08518b3ee08474
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74308543"
---
# <a name="failure-to-check-a-drivers-state"></a>无法检查驱动程序的状态





在以下示例中，驱动程序使用**ASSERT**宏来检查驱动程序映像的调试版本中是否有正确的设备状态，但不检查同一驱动程序源的零售版本中的设备状态：

```cpp
   case IOCTL_WAIT_FOR_EVENT:

      ASSERT((!Extension->WaitEventIrp));
      Extension->WaitEventIrp = Irp;
      IoMarkIrpPending(Irp);
      status = STATUS_PENDING;
```

在调试驱动程序映像中，如果驱动程序已经持有 IRP 挂起，系统将断言。 但在零售版本中，驱动程序不会检查此错误。 对相同 IOCTL 的两次调用会导致驱动程序失去 IRP 跟踪。

在多处理器系统上，此代码片段可能会导致其他问题。 假设在条目上，此例程拥有（操作权限）此 IRP 的所有权。 当例程将**irp**指针保存到全局结构中的**扩展&gt;WaitEventIrp**时，另一个线程可从该全局结构获取 IRP 地址并在 irp 上执行操作。 若要避免此问题，驱动程序应在保存 IRP 之前将 IRP 标记为 "挂起"，并且应包括对[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)的调用和互锁序列中的分配。 可能还需要 IRP 的[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程。

 

 




