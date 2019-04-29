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
ms.openlocfilehash: 2e5cc1286d49e4b6b48343b0248f83dc4bd46280
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364267"
---
# <a name="io-status-blocks"></a>I/O 状态块





I/O 状态块中，其中包括[ **IO\_状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff550671)结构，是属于每个[ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694). I/O 状态块有两个用途：

-   它提供了更高级别的驱动程序的[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)一种方式，确定服务工作完成 IRP 的例程。

-   它提供了有关为什么该服务的工作或不起作用的详细信息。

IRP，完成后**状态**字段指示是否处理 IRP 的驱动程序实际满足该请求或失败 IRP 具有错误状态。 **信息**字段提供有关实际发生了什么的详细信息的调用方。 例如，它包含实际读取或写入操作完成后传输的字节数。

有关详细信息，请参阅[IRP 中设置 I/O 状态块](processing-irps-in-a-lowest-level-driver.md#ddk-setting-the-i-o-status-block-in-an-irp-kg)。

 

 




