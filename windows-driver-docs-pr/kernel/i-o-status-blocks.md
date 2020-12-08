---
title: I/O 状态块
description: I/O 状态块
keywords:
- Irp WDK 内核，i/o 状态块
- I/o 状态阻止 WDK 内核
- 状态阻止 WDK 内核
- IO_STATUS_BLOCK 结构
- 状态信息 WDK Irp
- Irp WDK 内核，状态信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ecf3b30cfb5bf15c7e1a0b120e44d10afaab045
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836933"
---
# <a name="io-status-blocks"></a>I/O 状态块





I/o 状态块由 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构组成，它是每个 [**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)的组成部分。 I/o 状态块有两个用途：

-   它提供更高级别的驱动程序的 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，用于确定在完成 IRP 后服务是否正常工作。

-   它提供了有关该服务工作或无效的原因的详细信息。

完成 IRP 后，" **状态** " 字段将指示处理 IRP 的驱动程序是否确实满足了该请求，或是否失败了 irp，并显示了错误状态。 **信息** 字段向调用方提供有关实际发生情况的详细信息。 例如，它包含在读或写操作后实际传输的字节数。

有关详细信息，请参阅 [设置 IRP 中的 I/o 状态块](processing-irps-in-a-lowest-level-driver.md#ddk-setting-the-i-o-status-block-in-an-irp-kg)。

 

