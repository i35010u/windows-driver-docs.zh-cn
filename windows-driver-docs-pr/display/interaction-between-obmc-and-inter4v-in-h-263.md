---
title: H.263 中 OBMC 与 INTER4V 之间的交互
description: H.263 中 OBMC 与 INTER4V 之间的交互
ms.assetid: 096c723d-ec16-49f7-acaa-62ed228338c3
keywords:
- 宏块 WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f32d6a331607ab68f79d5987feaa273e1c4233a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379901"
---
# <a name="interaction-between-obmc-and-inter4v-in-h263"></a>H.263 中 OBMC 与 INTER4V 之间的交互


## <span id="ddk_interaction_between_obmc_and_inter4v_in_h_263_gg"></span><span id="DDK_INTERACTION_BETWEEN_OBMC_AND_INTER4V_IN_H_263_GG"></span>


有关 H.263 的之间的交互的一些详细信息*OBMC*， *INTER4V*， *B*， *EP*，和 PB 帧中的 B 可能有所帮助：

-   H.263 标准没有当前配置将执行这种情况在其**bPicOBMC**等于 1， *Motion4MV*等于 1，并*MotionBackward*等于 1。

-   不能在 H.263 B 或 EP 图片中使用 OBMC。

-   不能在 H.263 PB 图片的 B 部分使用 OBMC。

-   不能在 H.263 B 或 EP 图片中使用 INTER4V。

-   如果 INTER4V H.263 P 图片的宏块中使用，此宏块更高版本作为用于引用宏块 H.263 B 图片中的"直通"预测 OBMC 不直接预测中使用。 这是因为四个运动向量使用根据 H.263 附录 M，它可使用这些 H.263 附录 G，这不适用于 OBMC 等。 H.263 从不需要 OBMC 和向后的同一时间预测和永远不会使用 INTER4V 中向后方向。

### <a name="span-iddwmbsnlspanspan-iddwmbsnlspanspan-iddwmbsnlspandwmbsnl"></a><span id="dwMB_SNL"></span><span id="dwmb_snl"></span><span id="DWMB_SNL"></span>dwMB\_SNL

**DwMB\_SNL**结构成员指定已跳过宏块以下当前宏块，生成的数，并指明当前的块的残留的差异数据的位置宏块。 此成员包含两个变量：*MBskipsFollowing*中最明显的 8 位并*MBdataLocation*中最不重要的 24 位。 *MBskipsFollowing*指示已跳过宏块为其生成以下当前宏块的数目。 *MBdataLocation*是残留差异块数据缓冲区的索引。 此索引指示当前宏块，表示为 32 位的倍数的块的残留的差异数据的位置。

每个已跳过宏块为由*MBskipsFollowing*必须以数学上等效于递增的值的方式生成**wMBaddress** ，然后重复相同的宏块控制命令。

一个非零值与任何宏块控制命令*MBskipsFollowing*指定为要跳过，每个宏块执行经过运动补偿预测的方式，等效 (除外的值*MBskipsFollowing*) 显式非规范的第一个生成的已跳过宏块的一系列。 因此，每当*MBskipsFollowing*零，以下结构成员和变量必须全部为等于零不是：*Motion4MV IntraMacroblock* **wPatternCode** *并* **wPCOverflow**。

*MBdataLocation*变量必须为零宏块控制命令缓冲区中第一个宏块。 *MBdataLocation*可能包含任何值，如果**wPatternCode**为零。 当**wPatternCode**为零，解码器是建议但不是需要将此值设置为零或为相同的值相同的下一步的宏块控制命令。

有关生成已跳过宏块的详细信息，请参阅[生成跳过块效应](generating-skipped-macroblocks.md)。

### <a name="span-idwpatterncodespanspan-idwpatterncodespanspan-idwpatterncodespanwpatterncode"></a><span id="wPatternCode"></span><span id="wpatterncode"></span><span id="WPATTERNCODE"></span>wPatternCode

**WPatternCode**结构成员指示宏块中的每个块是否发送残留的差异数据。

位 (11-*我*) 的**wPatternCode** （其中位零是最低有效位） 指示块是否发送残留的差异数据*我*，其中*我*是为 mpeg-2 视频图中指定宏块中的块的索引，6-10、 6-11 和 6 到 12 (光栅扫描顺序为 Y 后, 跟 4:2:0 块的光栅扫描顺序 Cb 跟 4:2:0 块的 Cr，跟 4: Cb，2:2 块跟 4:2:2 块的 Cr，跟 4:4:4 块 Cb，跟 4:4:4 块的 Cr)。 编码的块的数据 (具有位 11-这些块*我*等于 1) 编码缓冲区相同的索引顺序中的剩余中找到 (增加*我*)。 4:2:0 mpeg-2 数据、 的值**wPatternCode**对应于转移 CBP （编码块模式） 的已解码的值向左旋转 6 位位置 (这些较低的位位置用于 4:2:2 和 4:4:4 色度格式)。

如果**bConfigSpatialResidInterleaved**的成员[ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)为 1，以发送基于主机的残留差异匹配的使用的 YUV 像素格式色度交错窗体。 在这种情况下，每个 Cb 并且在空间上相对应的块的 Cr 对将被视为单个残留差异结构单元的影响。 这不会更改值或的含义**wPatternCode**，但这意味着，Cb 和 Cr 数据块发送的每个对这两个成员时这些数据块的任何一个具有相应的位 （位 7 或位 6） 中设置**wPatternCode**。 如果中的位**wPatternCode**对应的残留的差异数据值的特定数据块为零，必须作为零配对 Cb 和 Cr 块要求发送残留的差异数据块时发送带的块**wPatternCode**位等于零。

 

 





