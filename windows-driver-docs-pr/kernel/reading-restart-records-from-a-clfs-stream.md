---
title: 从 CLFS 流读取重启记录
description: 从 CLFS 流读取重启记录
ms.assetid: 310545f6-d10d-481e-829d-287b045b98cd
keywords:
- 公用日志文件系统 WDK 内核，重新启动记录
- CLFS WDK 内核，重新启动记录
- 重新启动记录 WDK CLFS
- 读取重新启动记录
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b77faf2fac5f6805b9a50f7709b25e07876fb1e
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189491"
---
# <a name="reading-restart-records-from-a-clfs-stream"></a>从 CLFS 流读取重启记录





若要以相反顺序) 读取公用日志文件系统 (CLFS) stream (中的所有重新启动记录，请使用以下过程。

1.  调用 [**ClfsReadRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadrestartarea) 以获取读取上下文和最近写入到流中的重新启动记录。

2.  将你在步骤1中获取的读取上下文传递到重复 [**ClfsReadPreviousRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadpreviousrestartarea) 以获取日志中的剩余重新启动记录。

**注意**   当你调用[**ClfsWriteRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)将重启记录写入流时，CLFS 会自动将该记录的前一个 lsn 设置为流中上一次重新启动记录的 lsn。 前面的 Lsn 将形成链，然后再次调用对 **ClfsReadPreviousRestartArea**的调用。

 

 

