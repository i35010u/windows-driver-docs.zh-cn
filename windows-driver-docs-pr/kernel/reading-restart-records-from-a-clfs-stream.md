---
title: 从 CLFS 流读取重启记录
description: 从 CLFS 流读取重启记录
ms.assetid: 310545f6-d10d-481e-829d-287b045b98cd
keywords:
- 常见日志文件系统 WDK 内核，重新启动记录
- CLFS WDK 内核，重新启动记录
- 重新开始记录 WDK CLFS
- 读取重新开始记录
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffe2dc6ce2237c561d18a8715534d37067541da4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378757"
---
# <a name="reading-restart-records-from-a-clfs-stream"></a>从 CLFS 流读取重启记录





若要读取的所有公用日志文件系统 (CLFS) 流中重新启动记录 （按相反的顺序），使用以下过程。

1.  调用[ **ClfsReadRestartArea** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadrestartarea)获取读取的上下文和最近向流中写入重新开始记录。

2.  传递到步骤 1 中获取的读取的上下文[ **ClfsReadPreviousRestartArea** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfsreadpreviousrestartarea)反复获取剩余重新开始记录日志中。

**请注意**  当你调用[ **ClfsWriteRestartArea** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)若要重新开始记录写入流，CLFS 自动设置该记录的上一个 LSN 为的上一个 LSN在流中重新启动记录。 这些上一个 Lsn 形成后跟重复调用链**ClfsReadPreviousRestartArea**。

 

 

 




