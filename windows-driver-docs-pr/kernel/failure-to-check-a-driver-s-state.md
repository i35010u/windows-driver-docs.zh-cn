---
title: 无法检查驱动程序的状态
description: 无法检查驱动程序的状态
keywords:
- 可靠性 WDK 内核，驱动程序状态检查
- 检查驱动程序状态
- 驱动程序状态检查
- 验证驱动程序状态
- 正确的设备状态 WDK 内核
- 设备状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8773c3babd18c98de644f8a57b18fa1429bbcd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793557"
---
# <a name="failure-to-check-a-drivers-state"></a>无法检查驱动程序的状态





在以下示例中，驱动程序使用 **ASSERT** 宏来检查驱动程序映像的调试版本中是否有正确的设备状态，但不检查同一驱动程序源的零售版本中的设备状态：

```cpp
   case IOCTL_WAIT_FOR_EVENT:

      ASSERT((!Extension->WaitEventIrp));
      Extension->WaitEventIrp = Irp;
      IoMarkIrpPending(Irp);
      status = STATUS_PENDING;
```

在调试驱动程序映像中，如果驱动程序已经持有 IRP 挂起，系统将断言。 但在零售版本中，驱动程序不会检查此错误。 对相同 IOCTL 的两次调用会导致驱动程序失去 IRP 跟踪。

在多处理器系统上，此代码片段可能会导致其他问题。 假设在条目上，此例程拥有 (操作) 此 IRP 的权限。 当例程将 **irp** 指针保存在 **&gt; WaitEventIrp** 的全局结构中时，另一个线程可从该全局结构获取 irp 地址并在 irp 上执行操作。 若要避免此问题，驱动程序应在保存 IRP 之前将 IRP 标记为 "挂起"，并且应包括对 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 的调用和互锁序列中的分配。 可能还需要 IRP 的 [*取消*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel) 例程。

 

