---
title: 自定义的数据流压缩
description: 自定义的数据流压缩
ms.assetid: 7e42f3c7-c833-49ee-976b-ed32b921af95
keywords:
- Unidrv，数据传输压缩
- 数据传输压缩 WDK Unidrv
- 自定义的数据传输压缩 WDK Unidrv
- 压缩数据流 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8390c9690a2a1a8c314f47a257f1c21128640370
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372425"
---
# <a name="customized-data-stream-compression"></a>自定义的数据流压缩





Unidrv 可以执行数据压缩操作使用自定义的代码。 若要执行自定义的压缩操作，请执行以下步骤：

1.  提供用于实现的插件呈现[ **IPrintOemUni::Compression** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-compression)方法。

2.  在打印机中包含 CmdEnableOEMComp 命令输入*GPD*文件。

IPrintOemUni::Compression 方法作为输入接收扫描行数据。 该方法必须压缩的数据，然后将结果返回给 Unidrv。 **CmdEnableOEMComp**条目指定必须发送到打印机，以便打印机可以接受的压缩的数据的命令的命令。 对于每个扫描行中要发送到打印机，Unidrv 调用 IPrintOemUni::Compression 扫描行数据压缩。 然后，如果这是唯一可用的压缩方法，Unidrv 向打印机发送指定的命令**CmdEnableOEMComp**命令条目后, 跟压缩的数据。

如果打印机微型驱动程序包含 GPD 条目，还使 Unidrv 支持压缩方法，Unidrv 会尝试每个扫描行每种压缩算法，并选择生成最佳结果的算法。 有关 Unidrv 的压缩功能的详细信息，请参阅[压缩光栅数据](compressing-raster-data.md)。

可以一次启用只有一个自定义的压缩方法。

 

 




