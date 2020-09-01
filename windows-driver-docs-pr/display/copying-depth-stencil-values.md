---
title: 复制深度模具值
description: 复制深度模具值
ms.assetid: b83d4e6d-5645-49ab-bbb0-c694f1410cba
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，复制深度-模具值
- 复制深度-模具值
- 深度-模具值 WDK 显示
- 模具值 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef90827e0a1c1450f7243230f2100e45bc19bc49
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064874"
---
# <a name="copying-depth-stencil-values"></a>复制深度模具值


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**Blt**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt) 函数，将深度模具值从视频内存复制到系统内存，反之亦然。 驱动程序和硬件必须执行所有驱动程序支持的不透明深度模具格式的格式转换， (即，除 D3DDDIFMT D 可锁定) [**之外的所有**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)格式（ \_ D 可锁定的格式）均为 \* \_ 以下任意格式：

-   D3DDDIFMT \_ D16 的 \_ 锁定

-   D3DDDIFMT \_ D32 的 \_ 锁定

-   D3DDDIFMT \_ D32F 的 \_ 锁定

-   D3DDDIFMT \_ S8 的 \_ 锁定

驱动程序将丢弃源格式中存在但目标格式不存在的任何通道 (深度或模具) 。 运行时不允许在不共享任何常见通道类型的深度模具图面之间进行复制。

驱动程序首先将源深度值转换为32位无符号整数值，然后将从32位无符号整数值转换为目标表示形式。 以下规则适用于这两种转换：

-   如果源深度值为浮点值，则会应用一个夹具到 \[ 0，1， \] 并将结果乘以 \_ MAX \_ UINT。

-   如果源是整数并且目标是较低的整数，则会删除最右侧的附加位。

-   如果源是整数并且目标是更高的精度整数，则最右边的额外位将从最左侧的有效位进行复制。

-   如果源是整数并且目标是浮点值，则将32位整数转换为浮点值，并将结果除以 \_ MAX \_ UINT。

驱动程序无需提供对 nonuniformly 分布式深度值的特殊处理。

驱动程序将源模具值扩展到8位整数 (即，驱动程序在左侧) 上使用零填充源模具值。 如果目标表示形式使用较低精度，则驱动程序应丢弃最重要的位来执行转换。

用户模式显示驱动程序必须支持任意 subrectangles 的深度模具副本。 但是，驱动程序不需要在深度模具副本期间执行镜像、拉伸或颜色键操作。 在深度模具副本过程中，会隐式地需要点采样。

 

