---
title: 宏块控制命令
description: 宏块控制命令
ms.assetid: be70ec8f-1821-4075-b5e3-b7574fbe4e27
keywords:
- 宏块 WDK DirectX va，因此命令
- DXVA_MBctrl_I_HostResidDiff_1
- DXVA_MBctrl_I_OffHostIDCT_1
- DXVA_MBctrl_P_HostResidDiff_1
- DXVA_MBctrl_P_OffHostIDCT_1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46432e442e4c41bfe2db8a1a490b86f698689ebe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533182"
---
# <a name="macroblock-control-commands"></a>宏块控制命令


## <span id="ddk_macroblock_control_commands_gg"></span><span id="DDK_MACROBLOCK_CONTROL_COMMANDS_GG"></span>


在压缩的图片解码过程中每个已解码的宏块生成受宏块控制命令结构。 有四个宏块控制命令结构中定义*dxva.h*标头文件：

[**DXVA\_MBctrl\_I\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563983)

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563989)

[**DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)

[**DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563997)

在中显式定义的结构*dxva.h*泛型设计用于在 DirectX 弗吉尼亚宏块控制命令的特殊情况 此常规设计的说明，请参阅[泛型窗体的宏块控制命令结构](generic-form-of-macroblock-control-command-structures.md)。

若要使用哪个宏块控制命令结构的选择基于图片要解码的类型以及如何对其进行解码。 以下结构成员和标志确定图片类型解码选项，并将使用这四个 DirectX VA 宏块控制结构：

-   **BPicIntra**， **bChromaFormat**， **bPicOBMC**， **bPicBinPB**， **bPic4MVallowed**和**bMV\_RPS**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构。

-   **BConfigResidDiffHost**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构。

-   *HostResidDiff*标志 (位中的 10 **wMBtype**的每个宏块控制结构的成员)。

这些结构成员和标志的值是以下各节中所示。

### <a name="span-iddxvambctrlihostresiddiff1spanspan-iddxvambctrlihostresiddiff1spanspan-iddxvambctrlihostresiddiff1spandxvambctrlihostresiddiff1"></a><span id="DXVA_MBctrl_I_HostResidDiff_1"></span><span id="dxva_mbctrl_i_hostresiddiff_1"></span><span id="DXVA_MBCTRL_I_HOSTRESIDDIFF_1"></span>DXVA\_MBctrl\_I\_HostResidDiff\_1

**DXVA\_MBctrl\_我\_HostResidDiff\_1**。 以下结构成员和标志必须等于所示的值：

-   **bPicIntra**必须等于 1 （内部图片）。

-   **bChromaFormat**必须等于 1 （4:2:0 采样）。

-   *HostResidDiff*必须等于 1 (基于主机的 IDCT)。

-   **bConfigResidDiffHost**必须等于 1 （基于主机的残留差异解码）。

### <a name="span-iddxvambctrlioffhostidct1spanspan-iddxvambctrlioffhostidct1spanspan-iddxvambctrlioffhostidct1spandxvambctrlioffhostidct1"></a><span id="DXVA_MBctrl_I_OffHostIDCT_1"></span><span id="dxva_mbctrl_i_offhostidct_1"></span><span id="DXVA_MBCTRL_I_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_I\_OffHostIDCT\_1

[ **DXVA\_MBctrl\_我\_OffHostIDCT\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563989)结构用于内部图片 4:2:0 采样非主机残留差异解码。 以下结构成员和标志必须等于所示的值：

-   **bPicIntra**必须等于 1 （内部图片）。

-   **bChromaFormat**必须等于 1 （4:2:0 采样）。

-   *HostResidDiff*必须等于零 (非主机 IDCT)。

-   **bConfigResidDiffHost**必须等于零 （非主机残留差异解码）。

### <a name="span-iddxvambctrlphostresiddiff1spanspan-iddxvambctrlphostresiddiff1spanspan-iddxvambctrlphostresiddiff1spandxvambctrlphostresiddiff1"></a><span id="DXVA_MBctrl_P_HostResidDiff_1"></span><span id="dxva_mbctrl_p_hostresiddiff_1"></span><span id="DXVA_MBCTRL_P_HOSTRESIDDIFF_1"></span>DXVA\_MBctrl\_P\_HostResidDiff\_1

[ **DXVA\_MBctrl\_P\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563993)结构用于与基于主机的残留差异解码 P 和 B 的图片。 不使用以下宏块控制进程：OBMC、 使用的每个宏块的四个动作矢量的 B 部分的 PB 照片和使用动作矢量引用照片选择。

以下结构成员和标志必须等于所示的值：

-   **bPicIntra**必须等于零 (用于解码*P 图片*并*B 图片*还是隐蔽动作矢量中的*我想象着让*)。

-   **bChromaFormat**必须等于 1 （4:2:0 采样）。

-   *HostResidDiff*必须等于 1 (基于主机的 IDCT)。

-   **bPicOBMC**必须等于零 (OBMC 不使用)。

-   **bMV\_RPS**必须等于零 （动作矢量引用图片的选择不使用）。

-   在至少一个**bPicBinPB** （在不使用 PB 帧运动补偿图 B） 和**bPic4MVallowed** （每个宏块不使用四个前向引用动作矢量） 必须等于零。

-   **bConfigResidDiffHost**必须等于 1 （基于主机的残留差异解码）。

### <a name="span-iddxvambctrlpoffhostidct1spanspan-iddxvambctrlpoffhostidct1spanspan-iddxvambctrlpoffhostidct1spandxvambctrlpoffhostidct1"></a><span id="DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="dxva_mbctrl_p_offhostidct_1"></span><span id="DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>DXVA\_MBctrl\_P\_OffHostIDCT\_1

[ **DXVA\_MBctrl\_P\_OffHostIDCT\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563997)结构用于 P 和 B 的图片，4:2:0 采样非主机残留差异解码。 不使用以下宏块控制进程：OBMC、 使用的每个宏块的四个动作矢量的 B 部分的 PB 照片和使用动作矢量引用照片选择。

以下结构成员和标志必须等于所示的值：

-   **bPicIntra**的成员**DXVA\_PictureParameters**或中的动作矢量在隐蔽*我图片*)。

-   **bChromaFormat**必须等于 1 （4:2:0 采样）。

-   *HostResidDiff*必须等于零 (非主机 IDCT)。

-   **bPicOBMC**必须等于零 (OBMC 不使用)。

-   **bMV\_RPS**必须等于零 （动作矢量引用图片的选择不使用）。

-   在至少一个**bPicBinPB** （在不使用 PB 帧运动补偿图 B） 和**bPic4MVallowed** （每个宏块不使用四个前向引用动作矢量） 必须等于零。

-   **bConfigResidDiffHost**必须等于零 （非主机残留差异解码）。

 

 





