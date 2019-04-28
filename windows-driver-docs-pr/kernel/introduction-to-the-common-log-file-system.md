---
title: 通用日志文件系统简介
description: 通用日志文件系统简介
ms.assetid: 2185d834-81f3-4bf9-afa6-897c1515f8b5
keywords:
- 有关常见日志文件系统的常见日志文件系统 WDK 内核
- CLFS WDK 内核，有关公用日志文件系统
- 日志记录服务 WDK CLFS
- 常见的日志文件系统 WDK 用户模式
- CLFS WDK 用户模式
- 记录 WDK CLFS
- 多路复用 WDK CLFS 日志
- 专用的日志 WDK CLFS
- 日志序列号 WDK CLFS
- Lsn WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2f61ec177cdab10e1d0219f450ed0860fc70aac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341443"
---
# <a name="introduction-to-the-common-log-file-system"></a>通用日志文件系统简介





公用日志文件系统 (CLFS) 是一种通用的日志记录服务，可由软件[*客户端*](clfs-terminology.md#kernel-clfs-term-client)在用户模式或内核模式中运行。 本文档讨论的内核模式下客户端 CLFS 接口。 用户模式接口的信息，请参阅 Microsoft Windows SDK 中的公用日志文件系统。

CLFS 恢复和隔离利用语义 (ARIES) 封装的算法的所有功能。 但是，CLFS 设备驱动程序接口 (DDI) 并不局限于支持 ARIES;它非常适合于各种日志记录方案。

高性能的任何事务日志的主要工作是允许日志客户端能够准确地重复历史记录。 CLFS 通过实现这一点到内存缓冲区的封送处理的客户端日志记录强制到稳定存储，然后读取记录重新打开请求。 请务必注意，一条记录就稳定的存储和保持不变的存储媒体后，CLFS 将能够在多个系统故障读取记录。

CLFS 支持专用日志和多路复用日志。 专用的日志中的单个[*流*](clfs-terminology.md#kernel-clfs-term-stream)的所有日志的客户端使用的日志记录。 （也称为通用日志） 的多路的日志有多个流。 每个流具有其自己的客户端和其自己的日志记录的封送处理的内存缓冲区，但所有这些缓冲区中的记录多路复用到一个队列并刷新到稳定存储上的单个日志。 多路复用允许多个流要合并的 I/O 操作数。

当客户端将流写入一条记录时，获取返回标识以供将来参考的日志记录的日志序列号 (LSN)。 分配给递增序列写入到特定流窗体的记录的 Lsn。 即，分配给写入到流记录的 LSN 大于始终分配给写入到该同一个流上一条记录的 LSN。

CLFS 提供封送处理、 刷新，以及检索日志记录的多个服务。 以下列表介绍了一些这些其他服务。

-   可以提前保留一组相关的日志记录的空间。 这意味着客户端可以继续进行事务知道 CLFS 将能够将追加到日志的所有说明事务记录。

-   CLFS 维护每个日志记录的标头。 客户端可以设置的标头，以创建链接的记录的更高版本按相反的顺序遍历链中的某些字段。

-   CLFS 刷新日志记录到稳定存储根据其策略，但还允许客户端强制的一组稳定的存储的日志记录。

-   CLFS 维护日志以及每个流的多路日志的元数据。 客户端可以查看元数据和设置的元数据的某些部分。

-   对于每个流，CLFS 维护基准 LSN 和客户端可以使用来描述流的活动部分的最后一个 LSN。

-   对于专用日志，CLFS 维护 （在客户端的请求） 客户端可用来跟踪已存档的日志部分存档尾数据。

研究 ARIES 可以最好地理解 CLFS （例如上, 一个 LSN 和记录标头的撤消的下一步 LSN 字段） 的某些功能。 有关 ARIES 的详细信息，请参阅以下文章。

-   C. Mohan、 Don Haderle、 Bruce Lindsay、 Hamid Pirahesh，Peter Schwarz *ARIES:支持细粒度锁定事务恢复方法，并使用预写日志记录的部分回滚*。

-   C. Mohan，*重复超出 ARIES 的历史记录*。

 

 




