---
title: 使用本机系统服务例程的 Nt 和 Zw 版本
description: 使用本机系统服务例程的 Nt 和 Zw 版本
ms.assetid: 89627ddb-621d-4d27-acd6-16308689165d
keywords:
- 本机系统服务 API WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d047d2e3c44e8ee7974b23477453fe2a866461a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381627"
---
# <a name="using-nt-and-zw-versions-of-the-native-system-services-routines"></a>使用本机系统服务例程的 Nt 和 Zw 版本


Windows 本机操作系统服务 API 实现为一系列在内核模式下运行的例程。 这些例程具有前缀开头的名称**Nt**或**Zw**。 内核模式驱动程序可以直接调用这些例程。 用户模式应用程序可以访问这些例程使用的系统调用。

但有少数例外，每个本机系统服务例程具有两个略有不同版本中，将类似的名称，但不同的前缀。 例如，调用[NtCreateFile](https://go.microsoft.com/fwlink/p/?linkid=157250)并[ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)执行类似的操作，并且，事实上，通过相同的内核模式系统例程提供服务。 对于从用户模式下，系统调用**Nt**并**Zw**版本例程的行为方式相同。 从内核模式驱动程序，调用**Nt**并**Zw**在如何处理在调用方传递到该例程的参数值的不同版本的例程。

内核模式驱动程序调用**Zw**版本的本机系统服务例程，以通知的例程的参数是来自受信任，内核模式源。 在这种情况下，该例程假定它可以在没有首先验证中安全地使用参数。 但是，如果参数可能是从用户模式下源或内核模式源，该驱动程序改为调用**Nt**版本的程序，以确定，调用线程的历史记录是否基于参数源自用户模式或内核模式中。 有关如何例程用于用户模式参数区分从内核模式的参数的详细信息，请参阅[ **PreviousMode**](previousmode.md)。

在用户模式应用程序调用**Nt**或**Zw**版本的本机系统服务例程，该例程始终将接收的参数视为来自用户模式下的源的值不受信任。 例程进行全面验证参数值之前使用的参数。 具体而言，该例程探测任何调用方提供的缓冲区来验证缓冲区位于有效的用户模式内存中并已正确对齐。

本机系统服务例程做出其他假设他们接收的参数。 如果一个例程接收到的内核模式驱动程序已分配的缓冲区的指针，该例程假定在系统内存，不在用户模式内存中已分配缓冲区。 如果例程接收在用户模式应用程序已打开的句柄，该例程将查找用户模式下句柄表中，而不是在内核模式句柄表的句柄。

在极少数情况下，参数值的含义与不同更重要的是从用户模式和内核模式下的调用之间。 例如， [ **ZwNotifyChangeKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566488)例程 (或其**NtNotifyChangeKey**对应) 具有输入参数，对*ApcRoutine*并*ApcContext*，这意味着不同的事物，具体取决于参数是否从用户模式或内核模式的源。 从用户模式下，调用*ApcRoutine*指向的 APC 例程并*ApcContext*指向操作系统在其调用 APC 例程时提供的上下文值。 从内核模式下，调用*ApcRoutine*指向[**工作\_队列\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_work_queue_item)结构和*ApcContext*指定由所述的工作队列项的类型**工作\_队列\_项**结构。

本部分包括以下主题：

[**PreviousMode**](previousmode.md)

[库和标头](libraries-and-headers.md)

[Zw 前缀是什么意思？](what-does-the-zw-prefix-mean-.md)

[指定访问权限](access-mask.md)

[NtXxx 例程](ntxxx-routines.md)

 

 




