---
title: H.263 中 OBMC 与 INTER4V 之间的交互
description: H.263 中 OBMC 与 INTER4V 之间的交互
ms.assetid: 096c723d-ec16-49f7-acaa-62ed228338c3
keywords:
- macroblocks WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4c04708b17b2f4444d9c1bab9bfb6ef649c5d82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840355"
---
# <a name="interaction-between-obmc-and-inter4v-in-h263"></a>H.263 中 OBMC 与 INTER4V 之间的交互


## <span id="ddk_interaction_between_obmc_and_inter4v_in_h_263_gg"></span><span id="DDK_INTERACTION_BETWEEN_OBMC_AND_INTER4V_IN_H_263_GG"></span>


有关 263's *OBMC*、 *INTER4V*、 *B*、 *EP*和 B 之间的交互的一些详细信息可能会有所帮助：

-   当前不会将**bPicOBMC**标准配置为，其中，" *Motion4MV* " 等于1，" *MotionBackward* " 等于1。

-   OBMC 不能用于 H-p B 或 EP 图片。

-   OBMC 不能用于 .H PB 图片的 B 部分。

-   INTER4V 不能用于 H-p B 或 EP 图片。

-   如果在 INTER4V P 图片的宏块中使用了 ""，并且稍后将此宏块用作 B 图片中的 "直接" 预测的参考宏块，则直接预测中不使用 OBMC。 这是因为，将根据 .H 附录 M 使用四个运动向量，这种方法使用的是类似于 OBMC 的方法。 H. 从不同时要求 OBMC 和向后预测，并且永远不会使用 INTER4V。

### <a name="span-iddwmb_snlspanspan-iddwmb_snlspanspan-iddwmb_snlspandwmb_snl"></a><span id="dwMB_SNL"></span><span id="dwmb_snl"></span><span id="DWMB_SNL"></span>dwMB\_SNL

**DwMB\_SNL**结构成员指定在当前宏块之后要生成的已跳过 macroblocks 的数目，并指示当前宏块块的剩余差值数据的位置。 此成员包含两个变量： *MBskipsFollowing*在最高有效的8位和*MBdataLocation*中，最低有效24位。 *MBskipsFollowing*指示要在当前宏块之后生成的已跳过 macroblocks 的数量。 *MBdataLocation*是残留差异块数据缓冲区中的索引。 此索引指示当前宏块的块的残留差异数据的位置，表示为32位的倍数。

*MBskipsFollowing*指示的每个已跳过的宏块必须以数学等效方式生成，以便递增**wMBaddress**的值，然后重复相同的宏块 control 命令。

任何带非零值的宏块 control 命令*都指定如何*对每个要跳过的宏块执行运动补偿预测，并等效（ *MBskipsFollowing*的值除外）到显式nonskip 指定的一系列跳过 macroblocks 的第一代。 因此，当*MBskipsFollowing*不为零时，以下结构成员和变量必须都等于零： *Motion4MV IntraMacroblock* **wPatternCode** *和* **wPCOverflow**。

宏块控件命令缓冲区中的第一个宏块的*MBdataLocation*变量必须为零。 如果**wPatternCode**为零， *MBdataLocation*可以包含任何值。 当**wPatternCode**为零时，建议使用解码器，但不要求将此值设置为零或与下一个宏块控件命令中相同的值。

有关生成跳过的 macroblocks 的详细信息，请参阅[生成跳过的 macroblocks](generating-skipped-macroblocks.md)。

### <a name="span-idwpatterncodespanspan-idwpatterncodespanspan-idwpatterncodespanwpatterncode"></a><span id="wPatternCode"></span><span id="wpatterncode"></span><span id="WPATTERNCODE"></span>wPatternCode

**WPatternCode**结构成员指示是否为宏块中的每个块发送残留差异数据。

位（11- *i*） of **wPatternCode** （其中位零是最小有效位），指示是否为 block *i*发送残留差额数据，其中*i*是在宏块中按 mpeg-2 视频指定的块的索引。图6-10、6-11 和6-12 （x 的光栅扫描顺序，后跟光栅扫描订单中的4:2:0 块，后跟的4:2:0 块，后跟 Cb 的4:2:2 块，后跟 cb 的4:2:2 块，后跟的4:4:4 块）。 用相同的索引顺序（增加*i*）在残留编码缓冲区中找到编码的块（其位 11-*i*等于1的块）的数据。 对于 4:2:0 MPEG-2 数据， **wPatternCode**的值对应于将 CBP （编码块模式）的已解码值向左移动六位位置（用于4:2:2 和4:4:4 色度格式的低位位置）。

如果[**DXVA\_ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)的**bConfigSpatialResidInterleaved**成员为1，则基于主机的残留差异将以与使用的 YUV 像素格式匹配的色度交错形式进行发送。 在这种情况下，每个 Cb 和空间上对应的 这不会改变**wPatternCode**的值或含义，但这意味着每当其中一个数据块具有在**wPatternCode**中设置的相应位（第7或第6位）时，就会发送每对 Cb 和 Cr 数据块的两个成员。 如果特定数据块的**wPatternCode**中的位为零，则当 Cb 和 Cr 块配对需要为块发送一个残留差异数据块，且该数据块具有**wPatternCode**位等于零。

 

 





