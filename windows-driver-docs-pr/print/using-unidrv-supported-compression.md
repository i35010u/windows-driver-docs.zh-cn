---
title: 使用 Unidrv 支持的压缩
description: 使用 Unidrv 支持的压缩
ms.assetid: feda6898-da2c-403f-a159-1423891f3dd5
keywords:
- 光栅数据压缩 WDK Unidrv
- 光栅数据 WDK Unidrv 压缩
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ba602f74762c59bcc83e4bab97bc033f93ab6ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568576"
---
# <a name="using-unidrv-supported-compression"></a>使用 Unidrv 支持的压缩





如果在 GPD 文件中包括 CmdEnableTIFF4 命令输入，Unidrv 使用 TIFF 4.0 压缩。

如果在 GPD 文件中包括 CmdEnableDRC 命令输入，Unidrv 使用金压缩。

如果包括 CmdEnableFE\_RLE 命令在 GPD 文件中，Unidrv 项使用 FE RLE 压缩。

如果您的打印机支持多个以下压缩方法之一，可以包含命令输入的每个受支持的方法。 对于每个扫描行，Unidrv 会尝试每个压缩算法，并选择会生成最压缩的结果的算法。 （您可以包含自定义的算法。 请参阅[使用自定义压缩](using-customized-compression.md)。)当 Unidrv 找到最佳算法时，它将扫描行数据压缩。 然后它将发送到打印机指定相应的命令条目后, 跟压缩数据的命令。

如果指定 CmdDisableCompression 命令项，然后压缩方法可用，无论 Unidrv 暂时禁用在遇到小于其压缩形式的未压缩的数据块时发送压缩的数据。

若要限制不必要的计算，不要启用压缩方法 （通过指定其命令输入） 如果此方法不大可能产生可用的结果。

对于大多数打印机，可以启用或禁用通过发送命令字符串之外的数据块接受的压缩数据。 当指定 CmdEnableTIFF4，CmdEnableDRC，CmdEnableFE\_RLE，和 CmdDisableCompression 条目将命令字符串包含有关这些打印机。

对于某些打印机 （通常东亚打印机），压缩选择命令使用 CmdSendBlockData 命令嵌入在发送的光栅数据。 当指定 CmdEnableTIFF4、 CmdEnableDRC 或 CmdEnableFE\_这些打印机的 RLE 条目不包括命令字符串。 相反，指定一个空的带引号的字符串来表示该命令。 这将告知 Unidrv 使用压缩，但不是发送单独的命令来启用它。 对于这些打印机，可以使用只有一个压缩算法。 不需要 CmdDisableCompression 条目，因为没有为 Unidrv 若要在这种情况下禁用压缩方法。

详细了解 CmdEnableTIFF4，CmdEnableDRC，CmdEnableFE\_RLE，和 CmdDisableCompression 条目，请参阅[光栅数据压缩命令](raster-data-compression-commands.md)。

有关 CmdSendBlockData 详细信息，请参阅[光栅数据发出命令](raster-data-emission-commands.md)。

 

 




