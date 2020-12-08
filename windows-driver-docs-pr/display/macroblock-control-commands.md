---
title: 宏块控制命令
description: 宏块控制命令
keywords:
- macroblocks WDK DirectX VA，命令
- DXVA_MBctrl_I_HostResidDiff_1
- DXVA_MBctrl_I_OffHostIDCT_1
- DXVA_MBctrl_P_HostResidDiff_1
- DXVA_MBctrl_P_OffHostIDCT_1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 725057466e7d848bc6b24a0eecdf015e12d20aff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813813"
---
# <a name="macroblock-control-commands"></a>宏块控制命令


## <span id="ddk_macroblock_control_commands_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMANDS_GG"></span>


压缩的图片解码过程中每个解码的宏块的生成由宏块控制命令结构控制。 在 *dxva* 头文件中定义了四个宏块控件命令结构：

[**DXVA \_ MBctrl \_ I \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1)

[**DXVA \_ MBctrl \_ I \_ OffHostIDCT \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_offhostidct_1)

[**DXVA \_ MBctrl \_ P \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)

[**DXVA \_ MBctrl \_ P \_ OffHostIDCT \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)

在 *dxva* 中显式定义的结构是用于 DirectX VA 中宏块控制命令的通用设计的特殊情况。 有关此泛型设计的说明，请参阅 [宏块控件命令结构的一般形式](generic-form-of-macroblock-control-command-structures.md)。

选择要使用的宏块控件结构的方式取决于要解码的图片类型以及解码方式。 以下结构成员和标志确定了图片类型、解码选项，以及将使用四个 DirectX VA 宏块控制结构中的哪一种：

-   [**BPic4MVallowed \_ bMV**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicIntra**、 **bChromaFormat**、 **bPicOBMC**、 **bPicBinPB**、 **DXVA** 和 **PictureParameters \_ RPS** 成员。

-   [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的 **bConfigResidDiffHost** 成员。

-   每个宏块控制结构) 的 **wMBtype** 成员中 (位10的 *HostResidDiff* 标志。

以下部分显示了这些结构成员和标志的值。

### <a name="span-iddxva_mbctrl_i_hostresiddiff_1spanspan-iddxva_mbctrl_i_hostresiddiff_1spanspan-iddxva_mbctrl_i_hostresiddiff_1spandxva_mbctrl_i_hostresiddiff_1"></a><span id="DXVA_MBctrl_I_HostResidDiff_1"></span><span id="dxva_mbctrl_i_hostresiddiff_1"></span><span id="DXVA_MBCTRL_I_HOSTRESIDDIFF_1"></span>DXVA \_ MBctrl \_ I \_ HostResidDiff \_ 1

[**DXVA \_ MBctrl \_ I \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1)结构用于包含基于主机的 *残留差别解码* 的图片。 以下结构成员和标志必须等于指示的值：

-   **bPicIntra**) 中的图片必须等于 1 (。

-   **bChromaFormat** 必须等于 1 (4:2:0 采样) 。

-   *HostResidDiff* 必须等于 1 (基于主机的 IDCT) 。

-   **bConfigResidDiffHost** 必须等于 1 (基于主机的残留差异解码) 。

### <a name="span-iddxva_mbctrl_i_offhostidct_1spanspan-iddxva_mbctrl_i_offhostidct_1spanspan-iddxva_mbctrl_i_offhostidct_1spandxva_mbctrl_i_offhostidct_1"></a><span id="DXVA_MBctrl_I_OffHostIDCT_1"></span><span id="dxva_mbctrl_i_offhostidct_1"></span><span id="DXVA_MBCTRL_I_OFFHOSTIDCT_1"></span>DXVA \_ MBctrl \_ I \_ OffHostIDCT \_ 1

[**DXVA \_ MBctrl \_ I \_ OffHostIDCT \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_offhostidct_1)结构用于包含4:2:0 采样，并具有脱离主机残留差别解码的图片。 以下结构成员和标志必须等于指示的值：

-   **bPicIntra**) 中的图片必须等于 1 (。

-   **bChromaFormat** 必须等于 1 (4:2:0 采样) 。

-   *HostResidDiff* 必须等于零 (IDCT) 。

-   **bConfigResidDiffHost** 必须等于零 (关外残留差异解码) 。

### <a name="span-iddxva_mbctrl_p_hostresiddiff_1spanspan-iddxva_mbctrl_p_hostresiddiff_1spanspan-iddxva_mbctrl_p_hostresiddiff_1spandxva_mbctrl_p_hostresiddiff_1"></a><span id="DXVA_MBctrl_P_HostResidDiff_1"></span><span id="dxva_mbctrl_p_hostresiddiff_1"></span><span id="DXVA_MBCTRL_P_HOSTRESIDDIFF_1"></span>DXVA \_ MBctrl \_ P \_ HostResidDiff \_ 1

[**DXVA \_ MBctrl \_ p \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)结构用于具有基于主机的残留差别解码的 p 和 B 图片。 不使用以下宏块控制进程： OBMC，对每个宏块使用四个运动向量，适用于一张图片的 B 部分，使用运动矢量引用图片选择。

以下结构成员和标志必须等于指示的值：

-   **bPicIntra** 在 *我的图片*) 中， *P picture* 和 *B picture* 或 concealment 运动矢量的必须等于零 (解码。

-   **bChromaFormat** 必须等于 1 (4:2:0 采样) 。

-   *HostResidDiff* 必须等于 1 (基于主机的 IDCT) 。

-   **bPicOBMC** 必须等于零 (未使用 OBMC) 。

-   **bMV \_RPS** 必须等于零， (未使用) 的运动矢量引用图片选择。

-   BPicBinPB 中至少有一个 **bPicBinPB** (B-不使用) 和 bPic4MVallowed (四个前向引用动作向量的每个宏块的 **bPic4MVallowed** ，) 必须等于零。

-   **bConfigResidDiffHost** 必须等于 1 (基于主机的残留差异解码) 。

### <a name="span-iddxva_mbctrl_p_offhostidct_1spanspan-iddxva_mbctrl_p_offhostidct_1spanspan-iddxva_mbctrl_p_offhostidct_1spandxva_mbctrl_p_offhostidct_1"></a><span id="DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="dxva_mbctrl_p_offhostidct_1"></span><span id="DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>DXVA \_ MBctrl \_ P \_ OffHostIDCT \_ 1

[**DXVA \_ MBctrl \_ p \_ OffHostIDCT \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)结构用于具有4:2:0 采样的 p 和 B 图片，并具有脱离主机残留的差异解码。 不使用以下宏块控制进程： OBMC，对每个宏块使用四个运动向量，适用于一张图片的 B 部分，使用运动矢量引用图片选择。

以下结构成员和标志必须等于指示的值：

-   [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicIntra** 成员必须等于) 中 *图片* 的 P 和 *B 图片* 或 concealment 运动向量 (解码。

-   **bChromaFormat** 必须等于 1 (4:2:0 采样) 。

-   *HostResidDiff* 必须等于零 (IDCT) 。

-   **bPicOBMC** 必须等于零 (未使用 OBMC) 。

-   **bMV \_RPS** 必须等于零， (未使用) 的运动矢量引用图片选择。

-   BPicBinPB 中至少有一个 **bPicBinPB** (B-不使用) 和 bPic4MVallowed (四个前向引用动作向量的每个宏块的 **bPic4MVallowed** ，) 必须等于零。

-   **bConfigResidDiffHost** 必须等于零 (关外残留差异解码) 。

