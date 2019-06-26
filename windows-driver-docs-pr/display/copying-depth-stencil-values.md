---
title: 复制深度模具值
description: 复制深度模具值
ms.assetid: b83d4e6d-5645-49ab-bbb0-c694f1410cba
keywords:
- 用户模式显示驱动程序 WDK Windows Vista 中，将深度模具的值复制
- 将深度模具的值复制
- 深度模具值 WDK 显示
- 模具值 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fef10356a68cd2894deeeecf89def6796f57c359
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370253"
---
# <a name="copying-depth-stencil-values"></a>复制深度模具值


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **Blt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)函数来复制深度模具值从视频内存复制到系统内存，反之亦然。 驱动程序和硬件必须执行格式转换，或对所有驱动程序支持的不透明的深度模具格式 (即，所定义的所有格式[ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)以外的枚举类型D3DDDIFMT\_D\*\_LOCKABLE)，或从任一以下格式：

-   D3DDDIFMT\_D16\_LOCKABLE

-   D3DDDIFMT\_D32\_LOCKABLE

-   D3DDDIFMT\_D32F\_LOCKABLE

-   D3DDDIFMT\_S8\_LOCKABLE

驱动程序将放弃任何通道 （深度或模具） 源格式提供，但目标格式中不存在。 在运行时不允许深度模具图面，不共享任何常见的通道类型之间进行复制。

该驱动程序首先会将源的深度值转换为 32 位无符号的整数的值，然后从为目标表示形式的 32 位无符号的整数值。 以下规则适用于这两个这些转换：

-   如果源深度值是浮点值，为 clamp \[0，1\]应用并将结果乘以\_最大\_UINT。

-   如果源是不可或缺，目标是精度较低的整数，则会删除最右侧的额外位。

-   如果源是不可或缺，目标是一个更高精度的整数，从左侧的最高有效位复制额外的最右侧位。

-   如果是不可或缺的来源和目标是浮点值，则 32 位整数转换为浮点值，并且结果除以\_最大\_UINT。

该驱动程序不需要提供特殊处理方式为均匀分布式的深度值。

该驱动程序将源模具值扩展到 8 位整数 （即，在左侧的源模具值与零驱动程序填充）。 如果目标表示形式使用较低的精度，则驱动程序应丢弃的最高有效位来执行此转换。

用户模式显示驱动程序必须支持任意 subrectangles 深度模具的副本。 但是，驱动程序不需要在深度模具复制过程中执行镜像、 stretch 或颜色键操作。 点采样期间深度模具副本是隐式必需的。

 

 





