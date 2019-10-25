---
title: 网络重定向程序和文件系统进程
description: 网络重定向程序和文件系统进程
ms.assetid: 01bdd0d4-d03e-4b3c-ab34-1d5909cde284
keywords:
- 内核网络重定向程序 WDK，文件系统进程
- 异步请求 WDK 网络重定向器
- IRP_MJ_WRITE
- 文件系统调度 WDK 网络重定向器
- FSD WDK 网络重定向器
- 缓冲 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2056e9416bc35179dcbdf0173741f07254700556
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841053"
---
# <a name="network-redirectors-and-the-file-system-process"></a>网络重定向程序和文件系统进程


文件系统驱动程序执行的大部分文件操作通常在用户的线程上下文中完成。 这些操作包括对文件系统的所有同步文件 i/o 调用。 在这些情况下，所有工作都是以内联方式完成的。 此操作可能会在内核中阻止，但会在同一线程上执行工作。 Windows 上的文件系统通常使用用户的线程上下文作为文件系统调度来调用此工作（FSD）。 大多数情况下，文件系统将尝试在 FSD 中完成其工作。

在某些情况下，应用程序不希望阻止（例如异步读取或异步写入）。 在这些情况下，需要将文件 i/o 操作调度到系统工作线程完成。 Windows 上的文件系统通常使用系统工作线程上下文作为文件系统进程（FSP）来调用此工作。 下面的异步 IRP\_MJ\_写入请求发送到网络小型重定向器的示例说明了需要使用 FSP 的情况。

若要执行异步 IRP\_MJ\_写入请求，RDBSS 或网络微型重定向程序需要获取文件对象的 FCB 资源（用于更改文件对象的同步对象）。 如果 FCB 资源已经由另一个线程占用，并且 RDBSS 或网络微型重定向程序尝试获取用户线程上下文（FSD）中的 FCB 资源，则此操作将会阻止。 不应阻止对文件系统的异步请求。 对于异步请求（例如，IRP\_MJ\_写入请求），文件系统驱动程序将首先检查所需资源是否可用（例如，网络小型重定向器的 FCB 资源）。 如果资源不可用，则文件系统驱动程序会将请求发送到工作队列，以供以后由系统工作线程（FSP）完成，文件系统从 FSD 线程返回状态\_"。 对于用户应用程序，FSD 将立即返回状态\_立即挂起，而实际工作会由 FSP 中的系统工作线程处理。

在文件系统驱动程序将工作发送到 FSP 之前，必须完成几个任务。 文件系统驱动程序需要从 FSD 中用户的线程捕获安全上下文，因为工作线程将完成工作。 RDBSS 会自动在[**RxFsdPostRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)例程中为网络小型重定向程序执行此功能。 每当网络微重定向器返回状态\_"**挂起"，** 并且 RX\_上下文结构设置为 " **TRUE**" 时，此例程由 RDBSS 调用。 如果将工作发送到工作队列，则文件系统驱动程序还必须确保用户缓冲区可供系统工作线程以后使用。 可以通过两种方法来完成此任务：

1.  文件系统驱动程序可以在发布到 FSP 之前将用户缓冲区映射到内核内存空间，以便可以在以后通过系统工作线程（FSP）访问缓冲区。 文件系统驱动程序通常使用的方法是在 FSP 中锁定用户缓冲区，因为在以后可以通过系统工作线程映射内存页。

2.  文件系统可以从 FSP 保存调用进程的线程，并且系统工作线程可以在 FSP 中附加到此调用进程。 使用[**KeStackAttachProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestackattachprocess)，系统工作线程会附加到用户的调用进程，并访问用户缓冲区，然后在完成工作时使用[**KeUnstackDetachProcess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-keunstackdetachprocess)从用户的调用进程中分离。

只要 RX\_上下文\_标志\_不\_\_PREPOSTING，就会使用[**RxFsdPostRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest)例程中的方法1自动锁定用户缓冲区，只要 RX 上下文标志RX\_上下文结构的成员。 将为以下请求锁定用户缓冲区：

-   IRP\_MJ\_DIRECTORY\_控件，其次要功能为 IRP\_MN\_查询\_目录

-   IRP\_MJ\_QUERY\_EA

-   只要次要函数不包括 IRP\_MN\_MDL，IRP\_MJ\_读取

-   IRP\_MJ\_集\_EA

-   只要次要函数不包括 IRP\_MN\_MDL，IRP\_MJ\_写入

方法2通常用于处理使用方法\_的 Irp，这种情况下，如果只传递并返回一小部分信息。 这些 Irp 包括：

-   IRP\_MJ\_DEVICE\_CONTROL

-   IRP\_MJ\_文件\_系统\_控件

-   IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL

RDBSS 仅支持对**MrxLowIoSubmit**运算数组的异步调用。 如果网络小型重定向程序要实现其他操作（例如，[**MRxQueryFileInfo**](https://docs.microsoft.com/windows-hardware/drivers/ifs/mrxqueryfileinfo)）作为异步调用，则网络小型重定向程序需要将请求发布到 FSP。 如果网络微重定向器接收到**MrxQueryFileInfo**的请求，并且该请求使用 RX\_上下文\_在 RX\_上下文结构的**Flags**成员中设置的 ASYNC\_OPERATION 位，则网络小型重定向程序需要若要将此请求发布到 FSP 进行异步操作。 在**MrxQueryFileInfo**例程的操作中，网络小型重定向器首先需要捕获用户线程的安全上下文，并将用户缓冲区映射到内核空间（或将系统工作线程设置为附加到用户的调用在 FSP 中执行时处理。 然后，网络小型重定向器会将 RX\_的**PostRequest**成员设置为**TRUE** ，并从 FSD 返回\_状态返回状态。 此工作由系统工作线程（FSP）通过 RDBSS 调度到工作队列进行操作。

 

 




