---
title: 使用 Unidrv 支持的压缩
description: 使用 Unidrv 支持的压缩
keywords:
- 光栅数据压缩 WDK Unidrv
- 压缩光栅数据 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe57d744d58a01f83fdfc9aee8b99197929d023f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785970"
---
# <a name="using-unidrv-supported-compression"></a>使用 Unidrv 支持的压缩





如果在 GPD 文件中包含 CmdEnableTIFF4 命令项，则 Unidrv 将使用 TIFF 4.0 压缩。

如果在 GPD 文件中包含 CmdEnableDRC 命令项，则 Unidrv 将使用金压缩。

如果在 \_ GPD 文件中包含 CmdEnableFE RLE 命令条目，则 Unidrv 将使用 FE-RLE 压缩。

如果打印机支持多种压缩方法，则可以为每个受支持的方法包含命令条目。 对于每个扫描行，Unidrv 将尝试每个压缩算法，并选择生成最多压缩结果的算法。  (还可以包括自定义算法。 请参阅 [使用自定义压缩](using-customized-compression.md)) 。在 Unidrv 找到最佳算法时，它会压缩扫描行数据。 然后，它会将相应命令条目指定的命令发送到打印机，后跟压缩后的数据。

如果指定 CmdDisableCompression 命令条目，则无论可用的压缩方法是什么，Unidrv 会在遇到小于压缩格式的未压缩数据块时暂时禁用发送压缩的数据。

若要限制不必要的计算，请不要通过指定 (的命令条目来启用压缩方法) 如果该方法不太可能产生可用的结果。

对于大多数打印机，可以通过在数据块外发送命令字符串来启用或禁用压缩数据的接受。 为这些打印机指定 CmdEnableTIFF4、CmdEnableDRC、CmdEnableFE \_ 和 CmdDisableCompression 条目时，请包含命令字符串。

对于某些打印机 (通常为东亚打印机) ，压缩选择命令嵌入到使用 CmdSendBlockData 命令发送的光栅数据中。 为这些打印机指定 CmdEnableTIFF4、CmdEnableDRC 或 CmdEnableFE \_ RLE 条目时，请不要包含命令字符串。 而是指定一个空的带引号的字符串来表示命令。 这会告诉 Unidrv 使用压缩，但不发送单独的命令来启用它。 对于这些打印机，只能使用一个压缩算法。 不需要 CmdDisableCompression 项，因为在这种情况下，Unidrv 不能关闭压缩。

有关 CmdEnableTIFF4、CmdEnableDRC、CmdEnableFE \_ RLE 和 CmdDisableCompression 条目的详细信息，请参阅 [光栅数据压缩命令](raster-data-compression-commands.md)。

有关 CmdSendBlockData 的详细信息，请参阅 [光栅数据发射命令](raster-data-emission-commands.md)。

 

 




