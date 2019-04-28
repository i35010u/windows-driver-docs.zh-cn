---
title: 概述
description: 概述
ms.assetid: 3b2895a2-9a2e-46eb-b8fb-47d6db4a1de0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee729166924cf60c7af642c2891c6e6e7745135d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352783"
---
# <a name="overview"></a>概述


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


机会锁或 oplock，提供一种机制，允许文件服务器客户端 （如那些利用 SMB 和 SMB2 协议） 来动态更改以一致的方式来提高性能并减少给定的文件或流的缓冲策略网络使用。 若要增加的远程文件操作的网络性能，客户端可以本地缓冲文件数据，以便减少或消除了需要发送和接收网络数据包。 例如，客户端可能不需要将信息写入到远程服务器上的文件如果客户端知道没有其他进程访问的数据。 同样，客户端可能会缓冲预读数据从远程文件，如果客户端知道没有其他进程正在对远程文件写入数据。 应用程序和驱动程序还可以使用 oplock 来以透明方式访问文件而不会影响其他应用程序可能需要使用这些文件。

文件系统 （例如 NTFS） 支持每个文件的多个数据流。 Oplock 授予对流句柄，这意味着操作适用于给定文件的打开流，一般情况下，对一个流的操作不会影响上的其他流 oplock。 有例外情况，显式如下所示。 不支持的文件系统的备用数据流，如 FAT，将"文件"时此文档是指"流"。

目前有八种不同类型的 oplock:

-   一个**级别 2** （或共享） oplock 指示有多个读取器的流和没有编写器。 这样可支持客户端读取缓存。

-   一个**级别 1** （或排他） oplock 允许客户端打开一个流以便独占访问权限，并允许客户端执行任意缓冲。 这支持客户端缓存中读取和写入缓存。

-   一个**批处理**oplock （还排他） 允许客户端使流保持打开状态的服务器上，即使客户端计算机上的本地访问器已关闭流。 这支持客户端需要反复打开并在批处理脚本执行过程中关闭同一文件中，如的方案。 客户端读取此支持缓存，写入缓存，并处理缓存。

-   一个**筛选器**oplock （还排他） 允许应用程序和文件系统筛选器 （包括微筛选器），打开并读取流数据，"返回"其他应用程序、 客户端，或同时尝试访问相同的流时的方法。 这支持客户端缓存中读取和写入缓存。

-   一个**读取**(R) oplock （共享） 指示有多个读取器的流和没有编写器。 这样可支持客户端读取缓存。

-   一个**读句柄**(RH) oplock （共享） 指示有多个读取器的流，没有编写器，并且，客户端可以保留流在服务器上打开即使客户端计算机上的本地访问器已关闭流。 这支持客户端缓存中读取并处理缓存。

-   一个**读写**(RW) oplock （独占） 允许客户端打开一个流以便独占访问权限，并允许客户端执行任意缓冲。 这支持客户端缓存中读取和写入缓存。

-   一个**读写句柄**(RWH) oplock （独占） 允许客户端使流保持打开状态的服务器上，即使客户端计算机上的本地访问器已关闭流。 客户端读取此支持缓存，写入缓存，并处理缓存。

在 Windows NT 3.1 中实施级别 1、 级别 2 和批处理 oplock。 在 Windows 2000 中添加了筛选器 oplock。 Windows 7 中添加了 R、 RH、 RW 和 RWH oplock。

某些 oplock 看起来非常相似。 特别是，R 看起来类似于第 2 级、 RW 看起来类似于第 1 级和 RWH 看起来类似于批处理。 （下文统称为"Windows 7 oplock"） R、 RH、 RW 和 RWH oplock 已添加到 Windows 7，以提供更大的灵活性，调用方来表示缓存的意图，并允许 oplock 中断和升级 (即，修改从一个级别到级别更高版本的缓存; oplock 状态例如，升级读取 oplock 到读写 oplock）。 这种灵活性不是可实现与 （下文统称为"旧 oplock"） 级别 2、 级别 1、 批处理和筛选器 oplocks。 稍后在本文档中讨论了 Windows 7 oplock 和旧 oplock 之间的差异。

在内核中实现 oplock 包的核心功能 (主要通过*FsRtlXxx*例程)。 文件系统调用此包在其文件系统中实现的机会锁功能。 本文档介绍内核 oplock 包时，NTFS 文件系统的互操作。 其他文件系统函数类似的方式，但可能有细微的差异。

在流句柄上授予 Oplock 时。 这意味着 oplock 获得打开一个给定的流。 从 Windows 7 开始，流句柄可以与之关联*oplock 密钥*，也就是说，用于标识属于多个句柄的 GUID 值相同的客户端缓存查看 （请参阅本主题后面的说明）。 可以显式提供 oplock 密钥 (到[ **IoCreateFileEx**](https://msdn.microsoft.com/library/windows/hardware/ff548283)) 时创建了句柄。 如果 oplock 密钥未显式指定当创建了句柄时，系统会将该句柄为具有与其关联的唯一机会锁密钥，以便其密钥将不同于其他任何句柄的任何其他密钥。 如果对已授予 oplock，以外的句柄上收到的文件操作和与 oplock 句柄关联的 oplock 密钥不同于与操作的句柄关联的密钥和该操作是与不兼容当前授予 oplock，然后该 oplock 已断开。 即使是相同的进程或线程执行不兼容的操作会中断 oplock。 例如，如果进程打开的流为其授予独占 oplock，并且在同一进程然后再次打开相同流，使用不同 （或无） oplock 密钥，排他 oplock 被窃立即。

请记住，oplock 注册表项存在对句柄，而它们"置于"句柄时创建了句柄。 即使在不授予任何 oplock，可以使用 oplock 密钥将句柄相关联。

**请注意**  更准确地说 oplock 密钥是与相关联[**文件\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff545834)指的是流句柄的结构。 这一区别很重要时复制句柄，例如与[DuplicateHandle](https://go.microsoft.com/fwlink/p/?linkid=124237)。 每个重复的句柄引用相同的基础**文件\_对象**结构。

 

 

 




