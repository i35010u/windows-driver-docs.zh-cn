---
title: 自定义的数据流压缩
description: 自定义的数据流压缩
ms.assetid: 7e42f3c7-c833-49ee-976b-ed32b921af95
keywords:
- Unidrv，数据流压缩
- 数据流压缩 WDK Unidrv
- 自定义数据流压缩 WDK Unidrv
- 压缩数据流 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93964f4a0185ed4c8068241db74424c4d04d7fb7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838008"
---
# <a name="customized-data-stream-compression"></a>自定义的数据流压缩





Unidrv 允许使用自定义代码执行数据压缩操作。 若要执行自定义的压缩操作，请执行以下步骤：

1.  提供实现[**IPrintOemUni：： Compression**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-compression)方法的呈现插件。

2.  在打印机的*GPD*文件中包含一个 CmdEnableOEMComp 命令项。

IPrintOemUni：： Compression 方法接收扫描行数据作为输入。 方法必须压缩数据，然后将结果返回到 Unidrv。 **CmdEnableOEMComp**命令条目指定必须发送到打印机的命令，以便打印机可以接受压缩的数据。 对于要发送到打印机的每个扫描行，Unidrv 将调用 IPrintOemUni：： Compression 来压缩扫描行数据。 然后，如果这是唯一可用的压缩方法，Unidrv 会将**CmdEnableOEMComp**命令条目指定的命令发送到打印机，后跟压缩后的数据。

如果打印机微型驱动程序包含同时启用 Unidrv 支持的压缩方法的 GPD 条目，则 Unidrv 将尝试每个扫描行的每个压缩算法，并选择产生最佳结果的算法。 有关 Unidrv 的压缩功能的详细信息，请参阅[压缩光栅数据](compressing-raster-data.md)。

一次只能启用一个自定义压缩方法。

 

 




