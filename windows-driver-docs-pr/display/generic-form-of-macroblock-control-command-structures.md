---
title: 普通表单的宏块控制命令结构
description: 普通表单的宏块控制命令结构
ms.assetid: 44009238-0a8e-4018-9b50-06729640f5e4
keywords:
- 宏块 WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cb8d6a9bd201341c4d06c19ebdbf2ae65fc3af6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534359"
---
# <a name="generic-form-of-macroblock-control-command-structures"></a>普通表单的宏块控制命令结构


## <span id="ddk_generic_form_of_macroblock_control_command_structures_gg"></span><span id="DDK_GENERIC_FORM_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURES_GG"></span>


在中显式定义了以下宏块控制结构*dxva.h*泛型设计用于在 DirectX VA 宏块控制命令的特殊情况：

[**DXVA\_MBctrl\_I\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563983)

[**DXVA\_MBctrl\_I\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563989)

[**DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)

[**DXVA\_MBctrl\_P\_OffHostIDCT\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563997)

这些结构表示仅最常使用的窗体的宏块控制命令。 可以创建其他宏块控制命令、 基于这些现有结构的设计，以允许驱动程序以支持其他视频解码元素并处理解码过程的不同配置。

本部分介绍用于创建控制命令的其他宏块用作的基础泛型宏块控制命令结构的成员。 在本部分中的宏块控制命令结构定义分为四个部分。

**请注意**  宏块控制命令是与 16 字节的内存的边界对齐，因此构造为单字节对齐方式打包的已打包的数据结构。

 

 

 





