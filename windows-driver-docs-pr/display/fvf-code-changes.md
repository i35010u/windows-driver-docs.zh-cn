---
title: FVF 代码更改
description: FVF 代码更改
keywords:
- FVF WDK Direct3D
- multimatrix 顶点混合 WDK Direct3D，FVF 代码更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b1f26df7687d7d4f88ab6527cdf7d1a49a5fe15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839931"
---
# <a name="fvf-code-changes"></a>FVF 代码更改


## <span id="ddk_fvf_code_changes_gg"></span><span id="DDK_FVF_CODE_CHANGES_GG"></span>


Multimatrix 顶点混合的关键 API 影响是将顶点混合权重参数添加到灵活顶点格式 (FVF) 的位置组件。 这些参数存储为32位 IEEE 单精度浮点数。 它们通过添加四个用于 FVF 代码的新位模式（D3DVFV \_ XYZB2、D3DVFV \_ XYZB3、D3DVFV \_ XYZB4 和 D3DVFV \_ XYZB5）在输入顶点数据中显示。

这些代码确定了其他可分配给其他用途的空间的 Dword，如粒子 radius 或雾化参数，具体取决于启用了哪些功能。

**注意**   如果指定的混合权重的数目小于当前正在混合的矩阵的数目，则分配给最后一个矩阵的权重将定义为 (1.0-Bt) ，其中，Bt 是该顶点的其他权重的总和。

 

 

 





