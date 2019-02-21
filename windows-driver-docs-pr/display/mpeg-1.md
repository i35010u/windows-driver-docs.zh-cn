---
title: MPEG-1
description: MPEG-1
ms.assetid: be4db8ea-98fa-4693-a2ff-888499e97f38
keywords:
- Mpeg-1 WDK DirectX VA
- 向后预测 WDK DirectX VA
- 双向预测 WDK DirectX VA
- 预测阻止 WDK DirectX VA
- 向后预测预测阻止 WDK DirectX VA
- 正向预测预测阻止 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1abfe22c8b8c7c34ef547b6d621ea7162d9459e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525571"
---
# <a name="mpeg-1"></a>MPEG-1


## <span id="ddk_mpeg_1_gg"></span><span id="DDK_MPEG_1_GG"></span>


Mpeg-1 视频标准的标题为 ISO/IEC 11172 2。 开发后 H.261，显著借用此标准。 Mpeg-1 标准没有循环筛选器。 相反，它使用简单的后半部分示例筛选器表示的帧比 H.261 支持的完整示例准确性之间移动的更精细精度。

添加了两个其他预测模式，双向和向后的预测。 这些预测模式需要一个额外的参考框架会缓冲。 双向预测模式计算的平均值进预测和向后预测预测块。 对于求平均值向前和向后预测块的算术是类似于创建的后半部分采样内插的预测块。 基本结构在其他方面与 H.261 相同。

 

 





