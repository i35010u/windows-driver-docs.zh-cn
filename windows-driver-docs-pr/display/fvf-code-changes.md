---
title: FVF 代码更改
description: FVF 代码更改
ms.assetid: d9db4356-570b-4e05-aec9-bf36e26e4570
keywords:
- FVF WDK Direct3D
- multimatrix 顶点混合 WDK Direct3D，FVF 代码更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e0a5cafe4915d6e2b67a3234e1054cabc2b7ee7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519649"
---
# <a name="fvf-code-changes"></a>FVF 代码更改


## <span id="ddk_fvf_code_changes_gg"></span><span id="DDK_FVF_CODE_CHANGES_GG"></span>


Multimatrix 顶点混合的关键 API 影响是顶点的混合到位置部分中的灵活顶点格式 (FVF) 的权重参数的补充。 这些参数存储为 32 位 IEEE 单精度浮点数。 它们为出现在输入的顶点数据由指示添加了四个新的位模式 FVF 代码：D3DVFV\_XYZB2、 D3DVFV\_XYZB3、 D3DVFV\_XYZB4 和 D3DVFV\_XYZB5。

这些代码标识或者可能向其他用户授权，如粒子 radius 已分配的空间或雾参数，具体取决于启用功能的额外 dword 值。

**请注意**  如果的 blend 权重指定数小于矩阵当前混合，则分配到最后一个矩阵的权重定义为 (1.0-Bₜ)，其中 Bₜ 是以该顶点的其他权重的总计数.

 

 

 





