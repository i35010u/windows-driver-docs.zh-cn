---
title: 使用自定义压缩
description: 使用自定义压缩
ms.assetid: 959c0015-4b31-4790-8d2b-26d6acc19ac7
keywords:
- 光栅数据压缩 WDK Unidrv
- 光栅数据 WDK Unidrv 压缩
- 自定义的光栅数据压缩 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4483c88b9d4958e3040d1e82fce33ef01686c898
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362739"
---
# <a name="using-customized-compression"></a>使用自定义压缩





如果你想要提供自定义的压缩算法，则包含 CmdEnableOEMComp 命令输入指定命令，使您的算法。 如果您的打印机可以禁用压缩功能，可以选择包括一个 CmdDisableCompression 条目来指定命令禁用压缩。 你还必须提供[呈现插件](rendering-plug-ins.md)实现[ **IPrintOemUni::Compression** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-compression)方法。

如果提供的自定义的压缩算法，您还可以启用使用 Unidrv 支持的算法。 对于每个扫描行，Unidrv 会尝试每个压缩算法，并选择会生成最压缩的结果的算法。 (有关 Unidrv 支持算法的信息，请参阅[Using Unidrv-Supported 压缩](using-unidrv-supported-compression.md)。)当 Unidrv 找到最佳算法时，它将扫描行数据压缩。 然后它将发送到打印机指定相应的命令条目后, 跟压缩数据的命令。

有关 CmdEnableOEMComp 和 CmdDisableCompression 条目的详细信息，请参阅[光栅数据压缩命令](raster-data-compression-commands.md)。

有关自定义压缩的详细信息，请参阅[自定义数据 Stream 压缩](customized-data-stream-compression.md)。

 

 




