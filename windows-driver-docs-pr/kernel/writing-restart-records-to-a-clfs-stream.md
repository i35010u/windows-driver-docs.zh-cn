---
title: 将重启记录写入 CLFS 流
description: 将重启记录写入 CLFS 流
ms.assetid: ae341d7e-37b2-4880-948c-e78e29278c64
keywords:
- 公用日志文件系统 WDK 内核，重新启动记录
- CLFS WDK 内核，重新启动记录
- 重新启动记录 WDK CLFS
- 检查点 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b9bda9a30f8f80e180c1183dbfa8c20accca299
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835568"
---
# <a name="writing-restart-records-to-a-clfs-stream"></a>将重启记录写入 CLFS 流





公用日志文件系统（CLFS）流中有两种类型的记录：数据记录和重新启动记录。 本主题说明如何将重新启动记录写入 CLFS 流。 有关如何编写数据记录的信息，请参阅将[数据记录写入到 CLFS 流](writing-data-records-to-a-clfs-stream.md)。

通常情况下，重新启动记录会定期写入流以创建检查点，以便在发生系统故障时更有效地进行恢复。 假设您已经创建了封送处理区域并写入了几个数据记录。 然后，可以通过调用[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)来编写重启记录。 通过设置*fFlags*参数，可以指定是将重新启动记录放置在 "封送" 区域的保留空间中还是在新分配的空间中。当 CLFS 将重新启动记录写入流时，它会自动将记录的前一个 LSN 设置为该流的先前写入的重新开始记录的 LSN。 这构成了一系列可按相反顺序进行遍历的重新启动记录。 有关读取重新启动记录链的信息，请参阅[从 CLFS 流中读取重新启动记录](reading-restart-records-from-a-clfs-stream.md)。

如果要将重新启动记录写入流并同时更改流的基本 LSN，请将**ClfsWriteRestartArea**的*plsnBase*参数设置为新的基 lsn。

 

 




