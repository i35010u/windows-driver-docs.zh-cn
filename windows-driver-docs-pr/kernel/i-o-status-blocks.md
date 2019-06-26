---
title: I/O 状态块
description: I/O 状态块
ms.assetid: 59147bd1-6cd7-4fbe-b7bc-52e09ab88576
keywords:
- Irp WDK 内核，I/O 状态数据块
- I/O 状态块 WDK 内核
- 状态块 WDK 内核
- IO_STATUS_BLOCK 结构
- WDK Irp 的状态信息
- Irp WDK 内核，状态信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d64f0b90d6105b0d8f8c6645d7e84492d2599e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371857"
---
# <a name="io-status-blocks"></a>I/O 状态块





I/O 状态块中，其中包括[ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)结构，是属于每个[ **IRP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_irp). I/O 状态块有两个用途：

-   它提供了更高级别的驱动程序的[ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)一种方式，确定服务工作完成 IRP 的例程。

-   它提供了有关为什么该服务的工作或不起作用的详细信息。

IRP，完成后**状态**字段指示是否处理 IRP 的驱动程序实际满足该请求或失败 IRP 具有错误状态。 **信息**字段提供有关实际发生了什么的详细信息的调用方。 例如，它包含实际读取或写入操作完成后传输的字节数。

有关详细信息，请参阅[IRP 中设置 I/O 状态块](processing-irps-in-a-lowest-level-driver.md#ddk-setting-the-i-o-status-block-in-an-irp-kg)。

 

 




