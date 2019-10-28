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
ms.openlocfilehash: 056b799928e6b6c1b4326a1c0bec463d76626232
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839034"
---
# <a name="copying-depth-stencil-values"></a>复制深度模具值


Microsoft Direct3D runtime 调用用户模式显示驱动程序的[**Blt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_blt)函数，将深度模具值从视频内存复制到系统内存，反之亦然。 驱动程序和硬件必须执行所有驱动程序支持的不透明深度模具格式的格式转换（即， [**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举类型定义的所有格式，D3DDDIFMT\_D\*\_可锁定）到，或者，任何以下格式：

-   D3DDDIFMT\_D16\_锁定

-   D3DDDIFMT\_D32\_锁定

-   D3DDDIFMT\_D32F\_锁定

-   D3DDDIFMT\_S8\_锁定

驱动程序会丢弃源格式中存在但目标格式不存在的任何通道（深度或模具）。 运行时不允许在不共享任何常见通道类型的深度模具图面之间进行复制。

驱动程序首先将源深度值转换为32位无符号整数值，然后将从32位无符号整数值转换为目标表示形式。 以下规则适用于这两种转换：

-   如果源深度值为浮点值，则应用 \[0，1\] 的夹具，并将结果乘以 \_MAX\_UINT。

-   如果源是整数并且目标是较低的整数，则会删除最右侧的附加位。

-   如果源是整数并且目标是更高的精度整数，则最右边的额外位将从最左侧的有效位进行复制。

-   如果源是整数并且目标是浮点值，则将32位整数转换为浮点值，并将结果除以 \_MAX\_UINT。

驱动程序无需提供对 nonuniformly 分布式深度值的特殊处理。

驱动程序将源模具值扩展到8位整数（即，驱动程序将在源模具值的左侧填充零）。 如果目标表示形式使用较低精度，则驱动程序应丢弃最重要的位来执行转换。

用户模式显示驱动程序必须支持任意 subrectangles 的深度模具副本。 但是，驱动程序不需要在深度模具副本期间执行镜像、拉伸或颜色键操作。 在深度模具副本过程中，会隐式地需要点采样。

 

 





