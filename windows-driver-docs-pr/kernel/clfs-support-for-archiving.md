---
title: 存档的 CLFS 支持
description: 存档的 CLFS 支持
ms.assetid: 5a07d7d2-4939-48f8-bd4c-855af61034fb
keywords:
- 常见日志文件系统 WDK 内核，存档
- CLFS WDK 内核存档
- 存档 WDK CLFS
- 非临时日志 WDK CLFS
- 存档尾数据 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2772bcd6ec7a7b23fd4beb0cef59cfeb6fef3de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343719"
---
# <a name="clfs-support-for-archiving"></a>存档的 CLFS 支持





公用日志文件系统 (CLFS) 支持通过维护存档尾数据的专用日志存档。 当您调用[ **ClfsCreateLogFile** ](https://msdn.microsoft.com/library/windows/hardware/ff540792)若要创建专用的日志，可以设置文件\_特性\_存档标志*fFlagsAndAttributes*参数来指定 CLFS 应保留日志存档尾数据。 为其 CLFS 保留存档尾数据的日志称为*非临时日志*。

假设您正在执行的事务对数据库和每个事务有几个更新，描述了日志记录。 特定事务已提交并已写入到稳定存储后，可能不需要任何更多说明该事务的日志记录。 它是的日志记录将不需要在发生系统故障时重新启动了恢复。 但是，如果数据库没有最近保存在不同的介质上保留数据库的稳定存储介质将失败，数据库更新可能会丢失。

上一段描述存档数据库记录，但在其他情况下，可能想要存档的日志记录。 在任一情况下，存档是客户端 （软件） 的责任。 您可以跟踪的存档设置的日志存档尾数据已完成。 存档尾数据是为其存档尚未已完成的最早记录的日志序列号 (LSN)。

非临时日志实际上有两个反面： 有一个基准 LSN，另一个存档尾数据标记的标记。 根据通过调用可以放置两个反面[ **ClfsAdvanceLogBase** ](https://msdn.microsoft.com/library/windows/hardware/ff540773) (或[ **ClfsWriteRestartArea**](https://msdn.microsoft.com/library/windows/hardware/ff541770))，并[ **ClfsSetArchiveTail**](https://msdn.microsoft.com/library/windows/hardware/ff541744)。 通常，基准 LSN 指向仍所需的事务回滚或重新启动恢复和存档尾指向为其存档未执行的最早记录的最早记录。 请注意，存档尾数据可能小于基准 LSN 或可能会大于基准 LSN。

当您调用时，基准 LSN 和存档尾数据很重要[ **ClfsReadNextLogRecord** ](https://msdn.microsoft.com/library/windows/hardware/ff541690)重复读取的记录由上一个 Lsn 链接链，撤消的下一步 Lsn，或者用户 Lsn。 **ClfsReadNextLogRecord**不会读取 LSN 小于存档尾数据和基准 LSN 的记录。 但是，它将读取 LSN 是存档尾数据与基准 LSN 之间的记录。 有关以下记录链的详细信息，请参阅[读取数据记录从 CLFS Stream](reading-data-records-from-a-clfs-stream.md)。

 

 




