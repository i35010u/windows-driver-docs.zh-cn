---
title: 将重启记录写入 CLFS 流
description: 将重启记录写入 CLFS 流
ms.assetid: ae341d7e-37b2-4880-948c-e78e29278c64
keywords:
- 常见日志文件系统 WDK 内核，重新启动记录
- CLFS WDK 内核，重新启动记录
- 重新开始记录 WDK CLFS
- 检查点 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb67d97a8dcb0a44b3dcd71a602e9b1b92a1afcf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374107"
---
# <a name="writing-restart-records-to-a-clfs-stream"></a>将重启记录写入 CLFS 流





有两种类型的公用日志文件系统 (CLFS) 流中的记录： 数据记录，并重新开始记录。 本主题说明如何将重启记录写入到 CLFS 流。 有关如何编写数据记录的信息，请参阅[CLFS Stream 将数据记录写入](writing-data-records-to-a-clfs-stream.md)。

通常情况下，重启记录将写入流定期创建检查点，可帮助使恢复发生系统故障时更高效。 假定已创建封送处理区域并写入多个数据记录。 然后可以通过调用编写重新开始记录[ **ClfsWriteRestartArea**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-clfswriterestartarea)。 通过设置*fFlags*参数，可以指定是否重新开始记录放在封送处理区域保留空间中或新分配的空间中。当 CLFS 将重新开始记录写入流时，它自动设置的记录的上一个 LSN 为该流之前写入的重新开始记录的 LSN。 该窗体重新启动记录可以按相反的顺序遍历的链。 有关读取的重新启动记录链的信息，请参阅[读取重新启动记录从 CLFS Stream](reading-restart-records-from-a-clfs-stream.md)。

如果你想要重新开始记录写入到流并将流的基准 LSN 更改一次，设置*plsnBase*的参数**ClfsWriteRestartArea**到新基类的 LSN。

 

 




