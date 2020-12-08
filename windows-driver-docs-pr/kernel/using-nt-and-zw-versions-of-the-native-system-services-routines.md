---
title: 使用本机系统服务例程的 Nt 和 Zw 版本
description: 使用本机系统服务例程的 Nt 和 Zw 版本
keywords:
- 本机系统服务 API WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f87b9c490d35ed0568b31b58545891502d5171d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816067"
---
# <a name="using-nt-and-zw-versions-of-the-native-system-services-routines"></a>使用本机系统服务例程的 Nt 和 Zw 版本


Windows native 操作系统服务 API 实现为在内核模式下运行的一组例程。 这些例程的名称以前缀 **Nt** 或 **Zw** 开头。 内核模式驱动程序可以直接调用这些例程。 用户模式应用程序可以通过使用系统调用来访问这些例程。

除了几个例外，每个本机系统服务例程有两个略有不同的版本，但前缀不同。 例如，对 [NtCreateFile](/windows/win32/api/winternl/nf-winternl-ntcreatefile) 和 [**ZwCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatefile) 的调用执行类似的操作，事实上，它是由相同的内核模式系统例程提供服务的。 对于用户模式下的系统调用，例程的 **Nt** 版本和 **Zw** 版本的行为相同。 对于来自内核模式驱动程序的调用，例程的 **Nt** 和 **Zw** 版本不同于它们处理调用方传递到例程的参数值的方式。

内核模式驱动程序调用本机系统服务例程的 **Zw** 版本，以通知例程参数来自受信任的内核模式源。 在这种情况下，例程假定它可以安全地使用参数，而无需首先对其进行验证。 但是，如果参数可能来自用户模式源或内核模式源，则驱动程序将调用例程的 **Nt** 版本，该版本根据调用线程的历史记录来确定参数是在用户模式下还是在内核模式下生成的。 有关例程如何区分内核模式参数中的用户模式参数的详细信息，请参阅 [**PreviousMode**](previousmode.md)。

当用户模式应用程序调用本机系统服务例程的 **Nt** 或 **Zw** 版本时，例程将始终将它接收的参数视为来自不受信任的用户模式源的值。 例程在使用参数之前对参数值进行全面验证。 具体而言，例程会探查调用方提供的所有缓冲区，以验证缓冲区是否位于有效的用户模式内存并正确对齐。

本机系统服务例程对它们接收的参数做出其他假设。 如果某个例程收到指向由内核模式驱动程序分配的缓冲区的指针，该例程将假定该缓冲区是在系统内存中分配的，而不是在用户模式内存中分配的。 如果例程收到用户模式应用程序打开的句柄，则例程将查找用户模式句柄表中的句柄，而不是内核模式句柄表中的句柄。

在少数情况下，参数值的含义在用户模式和内核模式调用之间的差异更大。 例如， [**ZwNotifyChangeKey**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwnotifychangekey) 例程 (或其 **NtNotifyChangeKey** 对应的) 具有一对输入参数 *ApcRoutine* 和 *ApcContext*，这些参数表示不同的项，具体取决于参数是来自用户模式源还是内核模式源。 对于用户模式的调用， *ApcRoutine* 指向 apc 例程， *ApcContext* 指向操作系统在调用 APC 例程时提供的上下文值。 对于从内核模式进行的调用， *ApcRoutine* 指向 [**工作 \_ 队列 \_ 项**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_work_queue_item) 结构， *ApcContext* 指定 **工作 \_ 队列 \_ 项** 结构所描述的工作队列项的类型。

本节包括下列主题：

[**PreviousMode**](previousmode.md)

[库和标头](libraries-and-headers.md)

[Zw 前缀是什么？](what-does-the-zw-prefix-mean-.md)

[指定访问权限](access-mask.md)

[NtXxx 例程](ntxxx-routines.md)

