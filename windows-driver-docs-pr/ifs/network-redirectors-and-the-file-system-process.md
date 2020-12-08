---
title: 网络重定向程序和文件系统进程
description: 网络重定向程序和文件系统进程
keywords:
- 内核网络重定向程序 WDK，文件系统进程
- 异步请求 WDK 网络重定向器
- IRP_MJ_WRITE
- 文件系统调度 WDK 网络重定向器
- FSD WDK 网络重定向器
- 缓冲 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ba19d11f8a9fc147edb7ec2763245239497d362
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808815"
---
# <a name="network-redirectors-and-the-file-system-process"></a>网络重定向程序和文件系统进程


文件系统驱动程序执行的大部分文件操作通常在用户的线程上下文中完成。 这些操作包括对文件系统的所有同步文件 i/o 调用。 在这些情况下，所有工作都是以内联方式完成的。 此操作可能会在内核中阻止，但会在同一线程上执行工作。 Windows 上的文件系统通常使用用户的线程上下文调用此工作，因为文件系统调度 (FSD) 。 大多数情况下，文件系统将尝试在 FSD 中完成其工作。

在某些情况下，应用程序不希望阻止 (异步读取或异步写入操作，例如) 。 在这些情况下，需要将文件 i/o 操作调度到系统工作线程完成。 Windows 上的文件系统通常使用系统工作线程上下文调用此工作，因为文件系统进程 (FSP) 。 下面的示例将 \_ \_ 发送到网络小型重定向程序的异步 IRP MJ 写入请求说明了需要使用 FSP 的情况。

若要执行异步 IRP \_ MJ \_ 写入请求，RDBSS 或网络微型重定向程序需要获取文件对象的 FCB 资源 (用于更改文件对象) 的同步对象。 当 FCB 资源已由另一个线程控制，或网络微型重定向程序尝试在用户的线程 (上下文) 中获取 FCB 资源时，将阻止此操作。 不应阻止对文件系统的异步请求。 对于 (IRP \_ MJ 写入请求的异步请求 \_ ，例如) ，文件系统驱动程序将首先检查是否 (网络小型重定向程序的 FCB 资源提供所需的资源，例如) 。 如果资源不可用，则文件系统驱动程序会将请求发送到工作队列，以供以后由 (FSP) 的系统工作线程完成，并且文件系统返回 \_ FSD 线程的挂起状态。 对于用户应用程序，FSD 将立即返回状态 " \_ 挂起"，而实际工作会由 FSP 中的系统工作线程处理。

在文件系统驱动程序将工作发送到 FSP 之前，必须完成几个任务。 文件系统驱动程序需要从 FSD 中用户的线程捕获安全上下文，因为工作线程将完成工作。 RDBSS 会自动在 [**RxFsdPostRequest**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest) 例程中为网络小型重定向程序执行此功能。 每当网络微重定向器 \_ 使用 RX 上下文结构的 **PostRequest** 成员 \_ 将设置为 **TRUE** 时，RDBSS 就会调用此例程。 如果将工作发送到工作队列，则文件系统驱动程序还必须确保用户缓冲区可供系统工作线程以后使用。 可以通过两种方法来完成此任务：

1.  文件系统驱动程序可以将用户缓冲区映射到内核内存空间，然后再将其发布到 FSP，以便 (FSP) 的系统工作线程可以访问这些缓冲区。 文件系统驱动程序通常使用的方法是在 FSP 中锁定用户缓冲区，因为在以后可以通过系统工作线程映射内存页。

2.  文件系统可以从 FSP 保存调用进程的线程，并且系统工作线程可以在 FSP 中附加到此调用进程。 使用 [**KeStackAttachProcess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestackattachprocess)，系统工作线程会附加到用户的调用进程，并访问用户缓冲区，然后在完成工作时使用 [**KeUnstackDetachProcess**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-keunstackdetachprocess) 从用户的调用进程中分离。

只要 rx 上下文 [**RxFsdPostRequest**](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxfsdpostrequest) \_ \_ 标志 \_ 无 \_ PREPOSTING \_ 所需位未在 rx 上下文结构的 **Flags** 成员中设置 \_ ，RDBSS 就会使用 RxFsdPostRequest 例程中的方法1自动锁定用户缓冲区。 将为以下请求锁定用户缓冲区：

-   Irp \_ MJ \_ 目录 \_ 控件，其中包含 IRP \_ MN \_ QUERY \_ DIRECTORY 的次要功能

-   IRP \_ MJ \_ 查询 \_ EA

-   \_ \_ 只要次要函数不包含 irp \_ MN \_ MDL，irp MJ 读取

-   IRP \_ MJ \_ 设置 \_ EA

-   \_ \_ 只要次要函数不包括 irp \_ MN \_ MDL，irp MJ 写入

方法2通常用于处理 \_ 在通常只传递和返回少量信息时使用方法的 irp。 这些 Irp 包括：

-   IRP\_MJ\_DEVICE\_CONTROL

-   IRP \_ MJ \_ 文件 \_ 系统 \_ 控制

-   IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL

RDBSS 仅支持对 **MrxLowIoSubmit** 运算数组的异步调用。 如果网络小型重定向程序想要 ([**MRxQueryFileInfo**](./mrxqueryfileinfo.md)实现其他操作，例如) 异步调用，则网络小型重定向程序需要将请求发布到 FSP。 如果网络小型重定向器接收到 **MrxQueryFileInfo** 的请求，并在 \_ \_ \_ rx 上下文结构的 **Flags** 成员中设置了 rx 上下文 ASYNC OPERATION bit \_ ，则网络小型重定向程序需要将此请求发布到 FSP 进行异步操作。 在 **MrxQueryFileInfo** 例程的操作中，网络小型重定向器首先需要捕获用户线程的安全上下文，并将用户缓冲区映射到内核空间 (或者将系统工作线程设置为在 FSP) 中执行时附加到用户的调用进程。 然后，网络小型重定向器会将 RX 上下文结构的 **PostRequest** 成员设置 \_ 为 **TRUE** ，并 \_ 从 FSD 返回 "挂起" 状态。  (FSP) 的系统工作线程将通过 RDBSS 将工作调度到工作队列进行操作。

 

