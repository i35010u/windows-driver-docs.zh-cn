---
title: Bob 反交错算法
description: Bob 反交错算法
keywords:
- bob 取消隔行扫描 WDK DirectX VA，算法
- 取消隔行扫描 WDK DirectX VA，bob，算法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bff89cc93cb2eefe9dda53f9506c7853ea965f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810447"
---
# <a name="bob-deinterlacing-algorithm"></a>Bob 反交错算法


## <span id="ddk_bob_deinterlacing_algorithm_gg"></span><span id="DDK_BOB_DEINTERLACING_ALGORITHM_GG"></span>


如果显示驱动程序实现了 DXVA [取消隔行扫描 DDI](./deinterlace-ddi.md)，则除了任何专有的取消隔行扫描算法以外，它还必须支持 bob 样式取消隔行扫描算法。 下面是 bob 样式的取消隔行扫描算法的说明：

输入是 (i，j) <sub>中</sub> 的字段 F，因此，0 &lt; = i &lt; = M-1，0 &lt; = j &lt; = N-1，其中 i 和 j 分别为行索引和列索引。

Output<sub>是 (i</sub> ，j) 大小2xMxN 的帧 F，因此，0 &lt; = i &lt; = 2M，0 = &lt; j &lt; = N-1，其中 i 和 j 分别是行和列索引。

如果 (<sub>i</sub> ，j) 为顶层字段：

![在取消隔行扫描 (时，j) 为排名靠前的算法的计算](images/bobtop.png)

如果 (<sub>i</sub> ，j) 为底部字段：

![在取消隔行扫描 (时，j) 为下一个字段时，用于说明 bob 算法的计算](images/bobbotom.png)

每个定义都使用有限脉冲响应 (杉树) 筛选器，其脉冲响应 h 长度为2K。 脉冲 response h 围绕其中点进行对称，因此，h ₋₍ k ₊₁₎ = hk，k = 0 到 K-1，

![阐释筛选器算法的计算](images/firfiltr.png)

Bob 样式取消隔行扫描的首选形式使用 K = 2 和 h ₀ = 9/16 (因此，h ₁ = 1/16) 。 此筛选器应作为 (9 \* (b + c) 实现 (a + d) + 8) &gt; &gt; 4，其中 a、b、c 和 d 是用于生成一个输出样本的四个输入样本。

 

