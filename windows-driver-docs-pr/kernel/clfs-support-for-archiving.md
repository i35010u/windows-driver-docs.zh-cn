---
title: 存档的 CLFS 支持
description: 存档的 CLFS 支持
keywords:
- 公用日志文件系统 WDK 内核，存档
- CLFS WDK 内核，存档
- 存档 WDK CLFS
- 非短暂日志 WDK CLFS
- 存档结尾 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56ecdacb4a649ea36b01ea86e4baaf1ec8c39fe8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825657"
---
# <a name="clfs-support-for-archiving"></a>存档的 CLFS 支持





公用日志文件系统 (CLFS) 通过保留存档尾部来支持专用日志的存档。 调用 [**ClfsCreateLogFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfscreatelogfile)创建专用日志时，可以设置 \_ FFLAGSANDATTRIBUTES 参数的文件属性 \_ 存档标志，以指定 CLFS *fFlagsAndAttributes* 应为日志保留存档结尾。 CLFS 维护存档结尾的日志称为 " *不短暂日志*"。

假设您要对数据库执行事务，并且每个事务都有日志记录描述的多个更新。 在特定事务提交并写入到稳定存储后，你可能不需要描述该事务的日志记录。 也就是说，在发生系统故障时，在重新启动恢复期间不需要日志记录。 但是，如果保存数据库的稳定存储介质出现故障，并且数据库最近未在不同的介质上存档，则数据库更新可能会丢失。

上一段介绍了存档数据库记录，但在其他情况下，你可能想要存档日志记录。 在任一情况下，存档都是 (软件) 的客户端的责任。 通过设置日志的存档结尾，可以跟踪已完成的存档。 存档尾是尚未完成其存档的最早记录 (LSN) 的日志序列号。

非短暂日志实际上有两个反面：一个由基本 LSN 标记，另一个由存档尾部标记。 可以通过调用 [**ClfsAdvanceLogBase**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsadvancelogbase) (或 [**ClfsWriteRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)) 和 [**ClfsSetArchiveTail**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfssetarchivetail)，将两个反面定位在适合的位置。 通常，基本 LSN 指向事务回滚或重新启动恢复时仍需要的最早记录，并且存档尾指向尚未执行存档的最早记录。 请注意，存档尾可能小于基本 LSN，或者它可能大于基 LSN。

当你重复调用 [**ClfsReadNextLogRecord**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadnextlogrecord) 来读取由上 lsn、undo-next lsn 或 user lsn 链接的记录链时，基本 LSN 和存档结尾非常重要。 **ClfsReadNextLogRecord** 不会读取其 LSN 小于存档结尾和基本 LSN 的记录。 但是，它将读取其 LSN 介于存档结尾和基 LSN 之间的记录。 有关以下记录链的详细信息，请参阅 [从 CLFS 流中读取数据记录](reading-data-records-from-a-clfs-stream.md)。

 

