---
title: 宏块控制命令
description: 宏块控制命令
ms.assetid: be70ec8f-1821-4075-b5e3-b7574fbe4e27
keywords:
- macroblocks WDK DirectX VA，命令
- DXVA_MBctrl_I_HostResidDiff_1
- DXVA_MBctrl_I_OffHostIDCT_1
- DXVA_MBctrl_P_HostResidDiff_1
- DXVA_MBctrl_P_OffHostIDCT_1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32fd7ef9f75f018eb0663fafff314a0a543dfb6e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840589"
---
# <a name="macroblock-control-commands"></a>宏块控制命令


## <span id="ddk_macroblock_control_commands_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMANDS_GG"></span>


压缩的图片解码过程中每个解码的宏块的生成由宏块控制命令结构控制。 在*dxva*头文件中定义了四个宏块控件命令结构：

[**DXVA\_MBctrl\_I\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1)

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_offhostidct_1)

[**DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)

[**DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)

在*dxva*中显式定义的结构是用于 DirectX VA 中宏块控制命令的通用设计的特殊情况。 有关此泛型设计的说明，请参阅[宏块控件命令结构的一般形式](generic-form-of-macroblock-control-command-structures.md)。

选择要使用的宏块控件结构的方式取决于要解码的图片类型以及解码方式。 以下结构成员和标志确定了图片类型、解码选项，以及将使用四个 DirectX VA 宏块控制结构中的哪一种：

-   [**BPic4MVallowed\_bMV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的**bPicIntra**、 **bChromaFormat**、 **bPicOBMC**、 **bPicBinPB**、 **DXVA**和**PictureParameters\_RPS**成员。

-   [**DXVA\_ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfigResidDiffHost**成员。

-   *HostResidDiff*标志（每个宏块控制结构的**wMBtype**成员中的位10）。

以下部分显示了这些结构成员和标志的值。

### <a name="span-iddxva_mbctrl_i_hostresiddiff_1spanspan-iddxva_mbctrl_i_hostresiddiff_1spanspan-iddxva_mbctrl_i_hostresiddiff_1spandxva_mbctrl_i_hostresiddiff_1"></a><span id="DXVA_MBctrl_I_HostResidDiff_1"></span><span id="dxva_mbctrl_i_hostresiddiff_1"></span><span id="DXVA_MBCTRL_I_HOSTRESIDDIFF_1"></span>DXVA\_MBctrl\_I\_HostResidDiff\_1

**DXVA\_MBctrl\_I\_HostResidDiff\_1**。 以下结构成员和标志必须等于指示的值：

-   **bPicIntra**必须等于1（照片内部）。

-   **bChromaFormat**必须等于1（4:2:0 采样）。

-   *HostResidDiff*必须等于1（基于主机的 IDCT）。

-   **bConfigResidDiffHost**必须等于1（基于主机的残留差别解码）。

### <a name="span-iddxva_mbctrl_i_offhostidct_1spanspan-iddxva_mbctrl_i_offhostidct_1spanspan-iddxva_mbctrl_i_offhostidct_1spandxva_mbctrl_i_offhostidct_1"></a><span id="DXVA_MBctrl_I_OffHostIDCT_1"></span><span id="dxva_mbctrl_i_offhostidct_1"></span><span id="DXVA_MBCTRL_I_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_I\_OffHostIDCT\_1

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_offhostidct_1)结构用于包含4:2:0 采样的包含离主机残留差异解码的图片。 以下结构成员和标志必须等于指示的值：

-   **bPicIntra**必须等于1（照片内部）。

-   **bChromaFormat**必须等于1（4:2:0 采样）。

-   *HostResidDiff*必须等于零（脱离主机 IDCT）。

-   **bConfigResidDiffHost**必须等于零（脱离主机剩余差解码）。

### <a name="span-iddxva_mbctrl_p_hostresiddiff_1spanspan-iddxva_mbctrl_p_hostresiddiff_1spanspan-iddxva_mbctrl_p_hostresiddiff_1spandxva_mbctrl_p_hostresiddiff_1"></a><span id="DXVA_MBctrl_P_HostResidDiff_1"></span><span id="dxva_mbctrl_p_hostresiddiff_1"></span><span id="DXVA_MBCTRL_P_HOSTRESIDDIFF_1"></span>DXVA\_MBctrl\_P\_HostResidDiff\_1

[**DXVA\_MBctrl\_p\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)结构用于具有基于主机的残留差别解码的 p 和 B 图片。 不使用以下宏块控制进程： OBMC，对每个宏块使用四个运动向量，适用于一张图片的 B 部分，使用运动矢量引用图片选择。

以下结构成员和标志必须等于指示的值：

-   **bPicIntra**的值必须等于零（对*P 图片*进行解码，并在我的*图片*中进行*B 图片*或 concealment 运动矢量）。

-   **bChromaFormat**必须等于1（4:2:0 采样）。

-   *HostResidDiff*必须等于1（基于主机的 IDCT）。

-   **bPicOBMC**必须等于零（未使用 OBMC）。

-   **bMV\_RPS**必须等于零（未使用运动矢量引用图片选项）。

-   至少一个**bPicBinPB** （0-不使用 PB 帧运动补偿中的 B 图）和**bPic4MVallowed** （每个未使用宏块的四个前向引用运动向量）都必须等于零。

-   **bConfigResidDiffHost**必须等于1（基于主机的残留差别解码）。

### <a name="span-iddxva_mbctrl_p_offhostidct_1spanspan-iddxva_mbctrl_p_offhostidct_1spanspan-iddxva_mbctrl_p_offhostidct_1spandxva_mbctrl_p_offhostidct_1"></a><span id="DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="dxva_mbctrl_p_offhostidct_1"></span><span id="DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_P\_OffHostIDCT\_1

[**DXVA\_MBctrl\_p\_OffHostIDCT\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)结构用于 p 和 B 图片，其中包含4:2:0 采样，并且具有离主机残留差异解码。 不使用以下宏块控制进程： OBMC，对每个宏块使用四个运动向量，适用于一张图片的 B 部分，使用运动矢量引用图片选择。

以下结构成员和标志必须等于指示的值：

-   **bPicIntra**成员： **DXVA\_PictureParameters**或 concealment 运动向量。

-   **bChromaFormat**必须等于1（4:2:0 采样）。

-   *HostResidDiff*必须等于零（脱离主机 IDCT）。

-   **bPicOBMC**必须等于零（未使用 OBMC）。

-   **bMV\_RPS**必须等于零（未使用运动矢量引用图片选项）。

-   至少一个**bPicBinPB** （0-不使用 PB 帧运动补偿中的 B 图）和**bPic4MVallowed** （每个未使用宏块的四个前向引用运动向量）都必须等于零。

-   **bConfigResidDiffHost**必须等于零（脱离主机剩余差解码）。

 

 





