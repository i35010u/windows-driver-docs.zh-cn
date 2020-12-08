---
title: 从 CLFS 流读取重启记录
description: 从 CLFS 流读取重启记录
keywords:
- 公用日志文件系统 WDK 内核，重新启动记录
- CLFS WDK 内核，重新启动记录
- 重新启动记录 WDK CLFS
- 读取重新启动记录
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4f39cd07d5f3a03b794cccba0dcf040b76fa3f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805355"
---
# <a name="reading-restart-records-from-a-clfs-stream"></a>从 CLFS 流读取重启记录





若要以相反顺序) 读取公用日志文件系统 (CLFS) stream (中的所有重新启动记录，请使用以下过程。

1.  调用 [**ClfsReadRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadrestartarea) 以获取读取上下文和最近写入到流中的重新启动记录。

2.  将你在步骤1中获取的读取上下文传递到重复 [**ClfsReadPreviousRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadpreviousrestartarea) 以获取日志中的剩余重新启动记录。

**注意**  当你调用 [**ClfsWriteRestartArea**](/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea) 将重启记录写入流时，CLFS 会自动将该记录的前一个 lsn 设置为流中上一次重新启动记录的 lsn。 前面的 Lsn 将形成链，然后再次调用对 **ClfsReadPreviousRestartArea** 的调用。

 

 

