---
title: 概述
description: 概述
ms.assetid: 3b2895a2-9a2e-46eb-b8fb-47d6db4a1de0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c7fa35f0624d3141040bed5ba32f6d4b36ccd41
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910532"
---
# <a name="overview"></a>概述


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


机会锁（或 oplock）提供了一种机制，使文件服务器客户端（例如，使用 SMB 和 SMB2 协议的客户端）以一致的方式动态更改给定文件或流的缓冲策略，以提高性能并减少网络使用。 为了增加远程文件操作的网络性能，客户端可以在本地缓冲文件数据，从而减少或消除发送和接收网络数据包的需要。 例如，如果客户端知道没有其他进程访问该数据，则客户端可能不必将信息写入远程服务器上的文件。 同样，如果客户端知道没有其他进程正在将数据写入远程文件，则客户端可能会从远程文件缓冲预读数据。 应用程序和驱动程序还可以使用 oplock 以透明方式访问文件，而不会影响可能需要使用这些文件的其他应用程序。

NTFS 等文件系统支持每个文件多个数据流。 Oplock 是对流句柄授予的，这意味着操作应用于文件的给定公开流，通常情况下，对一个流执行的操作不会影响另一个流上的 oplock。 此项有一些例外，如下所示。 对于不支持备用数据流的文件系统，如 FAT，请在本文档引用 "stream" 时考虑 "file"。

目前有8种不同类型的 oplock：

-   **级别 2** （或共享的） oplock 指示有多个流读取器，而没有写入方。 此功能支持客户端读取缓存。

-   **1 级**（或独占） oplock 允许客户端打开流以进行独占访问，并允许客户端执行任意缓冲。 此功能支持客户端读取缓存和写入缓存。

-   如果客户端计算机上的本地访问器已关闭流，则**批处理**oplock （也是排他）允许客户端在服务器上保留流。 这种情况下，客户端需要重复打开和关闭同一文件，例如在批处理脚本执行期间。 此功能支持客户端读取缓存、写入缓存和处理缓存。

-   **筛选器**oplock （也是独占的）允许应用程序和文件系统筛选器（包括 minifilters）打开和读取流数据，当其他应用程序、客户端或同时尝试访问同一流时，这种方法可以 "后退"。 此功能支持客户端读取缓存和写入缓存。

-   **读取**（R） oplock （共享）表示有多个流读取器，而没有写入方。 此功能支持客户端读取缓存。

-   **读取句柄**（RH） oplock （共享）指示有多个流读取器、没有编写器，并且即使客户端计算机上的本地访问器已关闭流，客户端仍可以在服务器上保留流。 此功能支持客户端读取缓存和处理缓存。

-   **读写**（RW） oplock （独占）允许客户端打开流以进行独占访问，并允许客户端执行任意缓冲。 此功能支持客户端读取缓存和写入缓存。

-   **读写句柄**（RWH） oplock （独占）允许客户端在服务器上保留流，即使客户端计算机上的本地访问器已关闭流也是如此。 此功能支持客户端读取缓存、写入缓存和处理缓存。

已在 Windows NT 3.1 中实现级别1、级别2和批处理 oplock。 在 Windows 2000 中添加了筛选器 oplock。 Windows 7 中添加了 R、RH、RW 和 RWH oplock。

有些 oplock 看起来非常相似。 特别是，R 看起来类似于 Level 2，类似于 Level 1，RWH 看起来类似于 Batch。 将 R、RH、RW 和 RWH oplock （称为 "Windows 7 oplock" 的下文）添加到了 Windows 7，为调用方提供更大的灵活性，使调用方能够表达缓存意图，并允许 oplock 中断和升级（即修改将状态从一个级别 oplock 到更大的缓存级别;例如，将读取 oplock 升级到读写 oplock。 这种灵活性不适用于级别2、级别1、批处理和筛选器 oplock （下文统称为 "legacy oplock"）。 本文档稍后将讨论 Windows 7 oplock 与旧版 oplock 之间的差异。

Oplock 包的核心功能在内核（主要是通过*FsRtlXxx*例程）中实现。 文件系统调入此包以在其文件系统中实现 oplock 功能。 本文档介绍 NTFS 文件系统如何与内核 oplock 包进行互操作。 其他文件系统的工作方式类似，但可能存在细微的差异。

Oplock 在流句柄上授予。 这意味着，对某个给定的流打开将授予 oplock。 从 Windows 7 开始，流句柄可以与*oplock 键*关联，即，用于标识属于同一客户端缓存视图的多个句柄的 GUID 值（请参阅本主题后面的说明）。 创建句柄时，可显式提供 oplock 项（到[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefileex)）。 如果创建句柄时未显式指定 oplock 键，系统会将该句柄视为具有与其关联的唯一 oplock 键，使其密钥不同于任何其他句柄上的其他任何密钥。 如果在不是被授权者的句柄上接收到文件操作，并且与 oplock 的句柄关联的 oplock 密钥不同于与操作的句柄关联的键，并且该操作与当前已授予 oplock，则会破坏 oplock。 即使 oplock 与执行不兼容操作的进程或线程相同，也会中断。 例如，如果某一进程打开一个流，其中向其授予了独占 oplock，并且该进程再次打开相同的流，则使用不同的（或不） oplock 键，将会立即中断独占 oplock。

请记住，oplock 项存在于句柄上，并在创建句柄时 "put" 句柄。 即使未授予任何 oplock，你也可以将句柄与 oplock 项关联。

**请注意**  ，更准确地说，oplock 密钥与流句柄引用的[**文件\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_object)结构相关联。 当复制句柄时，这种区别很重要，例如 with [DuplicateHandle](https://go.microsoft.com/fwlink/p/?linkid=124237)。 每个重复的句柄都引用相同的基础**文件\_对象**结构。

 

 

 




