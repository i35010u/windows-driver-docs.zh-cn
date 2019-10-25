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
ms.openlocfilehash: 8400c08bd37c8648e53a76abbe015e4f392d18f5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827575"
---
# <a name="reading-restart-records-from-a-clfs-stream"></a>从 CLFS 流读取重启记录





若要读取公用日志文件系统（CLFS）流中的所有重新启动记录（顺序相反），请使用以下过程。

1.  调用[**ClfsReadRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadrestartarea)以获取读取上下文和最近写入到流中的重新启动记录。

2.  将你在步骤1中获取的读取上下文传递到重复[**ClfsReadPreviousRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfsreadpreviousrestartarea)以获取日志中的剩余重新启动记录。

  **请注意**，在调用[**ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-clfswriterestartarea)以将重新启动记录写入流时，CLFS 会自动将该记录的前一个 lsn 设置为流中上一次重新启动记录的 lsn。 前面的 Lsn 将形成链，然后再次调用对**ClfsReadPreviousRestartArea**的调用。

 

 

 




