---
title: 网络重定向程序和文件系统进程
description: 网络重定向程序和文件系统进程
ms.assetid: 01bdd0d4-d03e-4b3c-ab34-1d5909cde284
keywords:
- 内核网络重定向程序 WDK，文件系统进程
- 异步请求 WDK 网络重定向程序
- IRP_MJ_WRITE
- 文件系统调度 WDK 网络重定向程序
- FSD WDK 网络重定向程序
- 缓冲区 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a914ddae53fd28edc569b09ee2e17df9abb9045
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520394"
---
# <a name="network-redirectors-and-the-file-system-process"></a>网络重定向程序和文件系统进程


通常在用户的线程上下文中完成的大多数文件操作执行的文件系统驱动程序。 这些操作包括的所有同步文件 I/O 调用到文件系统。 在这些情况下，所有工作完成内联。 该操作可能会阻止在内核中，但在同一线程上执行工作。 Windows 上的文件系统通常调用使用用户的线程上下文作为文件系统调度 (FSD) 此工作。 大多数情况下，文件系统将尝试完成 FSD 的其工作。

有某些情况的下，应用程序不需要阻止 （异步读取或异步写操作，例如）。 在这些情况下，文件 I/O 操作需要调度到系统工作线程完成。 Windows 上的文件系统通常会调用此工作使用作为文件系统进程 (FSP) 的系统工作线程上下文。 下面的示例的异步 IRP\_MJ\_写入请求发送到网络微型重定向说明了 FSP 需要使用的事例。

若要执行异步 IRP\_MJ\_写入请求、 RDBSS 或网络的最小重定向程序需要获取文件对象的 FCB 资源 （使用用于更改文件对象的同步对象）。 当 FCB 资源已被其他线程占用，RDBSS 或网络微型-重定向程序尝试获取 FCB 资源用户的线程上下文 (FSD) 中时，将会阻止此操作。 异步请求到文件系统不应阻止。 对于异步请求 (IRP\_MJ\_写请求，例如)，文件系统驱动程序将首先检查所需的资源是否可用 （网络微型重定向，例如 FCB 资源）。 如果资源不可用，则文件系统驱动程序的系统工作线程 (FSP) 发布到工作队列，以便稍后完成请求和文件系统将返回状态\_FSD 线程从 PENDING。 FSD 将状态返回到用户应用程序，\_挂起立即，而实际 FSP 的系统工作线程将处理工作。

文件系统驱动程序发布到 FSP 工作之前，必须完成几个任务。 文件系统驱动程序需要捕获从 FSD 中的用户的线程的安全上下文，因为将由系统工作线程完成工作。 RDBSS 中自动执行此[ **RxFsdPostRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff554472)例程的网络微型-重定向程序。 每当网络微型重定向返回状态时，此例程称为通过 RDBSS\_与 PENDING **PostRequest** RX 成员\_上下文结构设置为**TRUE**。 如果工作将被发布到工作队列，文件系统驱动程序还必须确保用户缓冲区将可供以后使用系统工作线程。 有两种方法来完成此任务：

1.  文件系统驱动程序可以将用户缓冲区映射到后再发布到 FSP 内核内存空间，以便可以通过系统工作线程 (FSP) 更高版本访问缓冲区。 常用的文件系统驱动程序的方法是在 FSP 锁定用户缓冲区，锁定内存页始终映射更高版本的系统工作线程。

2.  文件系统可以将 FSP 保存调用进程的线程和系统工作线程可以将附加到在 FSP 此调用进程。 使用[ **KeStackAttachProcess**](https://msdn.microsoft.com/library/windows/hardware/ff549659)，系统工作线程会将附加到用户的调用进程和访问用户缓冲区并从用户的调用进程使用然后分离[**KeUnstackDetachProcess** ](https://msdn.microsoft.com/library/windows/hardware/ff549677)完成工作。

RDBSS 自动锁定使用方法 1 中的用户缓冲区[ **RxFsdPostRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff554472)例程对大量 IRP 的请求只要 RX\_上下文\_标志\_否\_PREPOSTING\_需执行未设置位**标志**RX 成员\_上下文结构。 将以下请求锁定用户的缓冲区：

-   IRP\_MJ\_目录\_IRP 的次要函数控制\_MN\_查询\_目录

-   IRP\_MJ\_查询\_EA

-   IRP\_MJ\_读取长次要函数不包括 IRP\_MN\_MDL

-   IRP\_MJ\_SET\_EA

-   IRP\_MJ\_编写，只要次要函数不包括 IRP\_MN\_MDL

方法 2 通常用于处理使用方法的 Irp\_既时只有少量的信息是通常情况下传递和返回。 这些 Irp 将包括：

-   IRP\_MJ\_DEVICE\_CONTROL

-   IRP\_MJ\_FILE\_SYSTEM\_CONTROL

-   IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL

RDBSS 仅支持用于异步调用**MrxLowIoSubmit**操作的数组。 如果网络微型重定向希望执行其他操作 ([**MRxQueryFileInfo**](https://msdn.microsoft.com/library/windows/hardware/ff550770)，例如) 的异步调用，作为网络微型重定向需要将该请求发送 FSP。 如果网络微型重定向收到的请求**MrxQueryFileInfo**带有 RX\_上下文\_异步\_操作中的设置位**标志**RX 的成员\_上下文结构网络微型重定向需要发布到的异步操作 FSP 的此请求。 中的操作**MrxQueryFileInfo**例程，网络微型-重定向程序首先需要捕获用户的线程的安全上下文中并将用户缓冲区映射到内核空间 （或设置系统工作线程将附加到该用户的调用进程在 FSP 中执行时）。 然后设置网络微型重定向**PostRequest** RX 成员\_上下文结构到**TRUE**并返回状态\_FSD 从 PENDING。 工作会被调度通过 RDBSS 到操作的工作队列的系统工作线程 (FSP)。

 

 




