---
title: 宏块控制命令结构的通用格式
description: 宏块控制命令结构的通用格式
keywords:
- macroblocks WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 660b6d1facf2b72bfffb44dff6a43137e718bd9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832421"
---
# <a name="generic-form-of-macroblock-control-command-structures"></a>宏块控制命令结构的通用格式


## <span id="ddk_generic_form_of_macroblock_control_command_structures_gg"></span><span id="DDK_GENERIC_FORM_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURES_GG"></span>


以下在 *dxva* 中显式定义的宏块控制结构是通用设计的特殊情况，用于 DirectX VA 中的宏块控制命令：

[**DXVA \_ MBctrl \_ I \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_hostresiddiff_1)

[**DXVA \_ MBctrl \_ I \_ OffHostIDCT \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_i_offhostidct_1)

[**DXVA \_ MBctrl \_ P \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)

[**DXVA \_ MBctrl \_ P \_ OffHostIDCT \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)

这些结构仅表示最常使用的宏块控件命令形式。 基于这些现有结构的设计，可以创建其他宏块控制命令，以允许驱动程序支持其他视频解码元素和处理解码过程的不同配置。

本部分介绍通用宏块控件命令结构的成员，该结构用作创建其他宏块控件命令的基础。 本节中的宏块控制命令结构定义分为四个部分。

**注意**   宏块控件命令与16字节的内存边界对齐，并以单字节对齐方式打包构造为打包的数据结构。

 

 

