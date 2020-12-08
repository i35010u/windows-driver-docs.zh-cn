---
title: MPEG-1
description: MPEG-1
keywords:
- MPEG-2 WDK DirectX VA
- 向后预测 WDK DirectX VA
- 双向预测 WDK DirectX VA
- 预测块 WDK DirectX VA
- 向后预测预测块 WDK DirectX VA
- 向前预测预测块 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 778bc1ef0aaaf819fb5566eb31160c3c878f1753
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839587"
---
# <a name="mpeg-1"></a>MPEG-1


## <span id="ddk_mpeg_1_gg"></span><span id="DDK_MPEG_1_GG"></span>


MPEG-2 视频标准标题为 ISO/IEC 11172-2。 此标准是在261后开发的，并从它中得到了重大借用。 MPEG-2 标准没有循环筛选器。 相反，它使用简单的半示例筛选器，它表示帧之间移动的更精细度，而不是261支持的完全样本准确性。

添加了两个附加预测模式：双向预测和后向预测。 这些预测模式需要一个附加的引用帧进行缓冲。 双向预测模式将平均向前预测预测块和向后预测预测块。 用于计算正向和向后预测块的算法与创建半抽样内插预测块的算法类似。 基本结构与261相同。

 

 





