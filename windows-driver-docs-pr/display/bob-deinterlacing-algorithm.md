---
title: Bob 反交错算法
description: Bob 反交错算法
ms.assetid: ef3220bd-841d-4187-bc86-11b999eae2bd
keywords:
- bob 去隔行 WDK DirectX VA，算法
- 取消隔行扫描 WDK DirectX VA，bob、 算法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20cf5e3cbab2f267ddaf61e07947dd42ac0e078c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344634"
---
# <a name="bob-deinterlacing-algorithm"></a>Bob 反交错算法


## <span id="ddk_bob_deinterlacing_algorithm_gg"></span><span id="DDK_BOB_DEINTERLACING_ALGORITHM_GG"></span>


如果显示驱动程序实现 DXVA[去隔行 DDI](https://msdn.microsoft.com/library/windows/hardware/ff552701)，则它必须支持除了去隔行算法任何专有的 bob 样式取消隔行扫描算法。 下面是 bob 样式取消隔行扫描算法的说明：

输入是字段 F<sub>中</sub>（i，j） MxN 此类大小的 0 &lt;= i &lt;= M-1 和 0 &lt;= j &lt;= 的 N-1，其中 i 和 j 分别为行和列索引。

输出是帧 F<sub>出</sub>（i，j） 的此类大小 2xMxN 0 &lt;= i &lt;= 2 分 1 和 0 &lt;= j &lt;= 的 N-1，其中 i 和 j 分别为行和列索引。

如果 F<sub>在</sub>（i，j） 是顶级字段：

![说明如何去隔行算法时 fin(i,j) 是顶级字段 bob 计算](images/bobtop.png)

如果 F<sub>在</sub>（i，j） 是底部字段：

![说明如何去隔行算法时 fin(i,j) 是底部字段 bob 计算](images/bobbotom.png)

每个定义长度为 2 个 K h 脉冲响应与使用有限脉冲响应 (FIR) 过滤器。 脉冲响应 h 是对称操作，有关这样 h₋₍ₖ₊₁₎ = hₖ k = 0 到 K-1 和

![说明如何筛选器算法的计算](images/firfiltr.png)

Bob 样式去隔行的首选的形式使用 K = 2 和 h₀ = 9/16 (因此 h₁ = 1/16)。 应为实现此筛选器 (9\*(b+c)-(a+d)+8)&gt;&gt;4，其中 a、 b、 c 和 d 是用于生成一个输出示例的四个输入的示例。

 

 





