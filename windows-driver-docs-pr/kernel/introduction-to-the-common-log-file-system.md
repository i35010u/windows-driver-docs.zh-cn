---
title: 通用日志文件系统简介
description: 通用日志文件系统简介
keywords:
- 公用日志文件系统 WDK 内核，关于公用日志文件系统
- CLFS WDK 内核，关于公用日志文件系统
- 日志记录服务 WDK CLFS
- 公用日志文件系统 WDK 用户模式
- CLFS WDK 用户模式
- 记录 WDK CLFS
- 多路复用日志 CLFS
- 专用日志 WDK CLFS
- 日志序列号 WDK CLFS
- Lsn WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19156eedd373887c57c6f09729bb75b22b813536
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838875"
---
# <a name="introduction-to-the-common-log-file-system"></a>通用日志文件系统简介





公用日志文件系统 (CLFS) 是一种通用日志记录服务，可供在用户模式下运行的软件 [*客户端*](clfs-terminology.md#kernel-clfs-term-client) 或内核模式使用。 本文档讨论了用于内核模式客户端的 CLFS 接口。 有关用户模式接口的信息，请参阅 Microsoft Windows SDK 中的公用日志文件系统。

CLFS 封装算法的所有功能，以用于 (ARIES) 的恢复和隔离利用语义。 但是，CLFS 设备驱动程序接口 (DDI) 并不限于支持 ARIES;它很适合用于各种日志记录方案。

任何高性能事务日志的主要工作是允许日志客户端准确地重复历史记录。 CLFS 通过将客户端日志记录封送到内存缓冲区中，将其强制转换为稳定存储，并按请求读回记录，来实现此功能。 需要注意的是，在记录使其稳定存储并且存储媒体完好无损时，CLFS 将能够跨系统故障读取记录。

CLFS 支持专用日志和多路复用日志。 专用日志包含 [*一条日志*](clfs-terminology.md#kernel-clfs-term-stream) 记录，由日志的所有客户端使用。 多路日志 (也称为公共日志) 有多个流。 每个流都有自己的客户端和其自己的内存缓冲区用于封送日志记录，但所有这些缓冲区中的记录都可复用到一个队列中，并刷新到稳定存储上的单个日志。 多路复用允许合并多个流的 i/o 操作。

当客户端向流中写入记录时，它将返回一个日志序列号 (LSN) 用于标识日志记录以备将来参考。 分配给写入特定流的记录的 Lsn 将形成递增的序列。 也就是说，分配给写入到流中的记录的 LSN 总是大于分配给写入到该相同流的前一条记录的 LSN。

除了封送、刷新和检索日志记录外，CLFS 还提供多个服务。 以下列表描述了其中一些其他服务。

-   可以提前保留一组相关日志记录的空间。 这意味着客户端可以继续处理事务，知道 CLFS 将能够向日志追加描述事务的所有记录。

-   CLFS 维护每个日志记录的标头。 客户端可以在标头中设置某些字段，以创建链接记录的链，以后可以按相反的顺序进行遍历。

-   CLFS 根据日志记录的策略，将日志记录刷新到稳定存储，还允许客户端将一组日志记录强制到稳定的存储。

-   CLFS 维护日志的元数据以及多路复用日志的每个流。 客户端可以查看元数据并设置元数据的某些部分。

-   对于每个流，CLFS 维护一个基本 LSN 和最后一个 LSN，客户端可以使用该 LSN 来描绘流的活动部分。

-   对于专用日志，CLFS 在客户端的请求上维护 () 存档尾部，客户端可以使用该尾部跟踪已存档的日志部分。

CLFS 的某些功能 (例如，记录标头) 的前一个 LSN 和 undo 下一段 有关 ARIES 的详细信息，请参阅以下文章。

-   C. Mohan、堂 Haderle、Bruce Lindsay、Hamid Pirahesh、Peter Schwarz、 *ARIES：支持使用 Write-Ahead 日志记录 Fine-Granularity 锁定和部分回滚的事务恢复方法*。

-   C. Mohan， *重复的历史记录超出了 ARIES*。

 

 




