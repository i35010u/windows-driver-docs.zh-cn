---
title: KSPROPSETID\_Itd3d
description: KSPROPSETID\_Itd3d
ms.assetid: 87159be4-740e-47c9-b16f-16ca4d01c793
keywords:
- KSPROPSETID_Itd3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd2cb80d8c307059f79d463c1611bf2691ebbf6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830470"
---
# <a name="kspropsetid_itd3d"></a>KSPROPSETID\_Itd3d


## <span id="ddk_kspropsetid_itd3d_ks"></span><span id="DDK_KSPROPSETID_ITD3D_KS"></span>


`KSPROPSETID_Itd3d` 属性集用于配置3D 节点（[**KSNODETYPE\_3d\_效果**](ksnodetype-3d-effects.md)）使用的 interaural 时间延迟（ITD）算法。

从特定的声音源到达监听器的左侧和右侧的耳会按不同的数量延迟，具体取决于源的位置。 侦听器可以根据差异延迟量推断出声音源的方向。 ITD 算法控制差异延迟，以模拟3D 空间中特定位置处的声音源。

ITD 算法通过控制声音到达每个耳的量来提供附加的声音定位提示（muffled）。 可以 muffled 高频声音来模拟位于侦听器头后面的声音源。 例如，对于位于右耳附近的声音源，到达左耳的声音比到达正确的耳更 muffled。 Muffled 声音是通过将来自 sound 源的原始信号与相同信号的低传筛选版本组合在一起生成的。 Attenuating 原始信号，同时增加低传递筛选版本中的内容模拟将模拟声音源移到侦听器头后面的效果。

当声音源的位置发生更改时，必须更新以下参数：

-   声音到达每个耳的延迟量。

-   声音到达每个耳的量为 muffled。

对这些参数进行即时更改可能导致单击和其他虚假噪音。 ITD 算法通过多个样本对这些参数进行平滑转换，以便筛选出此类噪音。

有关 ITD 算法使用的参数的详细信息，请参阅[**KSDS3D\_ITD\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksds3d_itd_params)。

此属性集只包含一个属性：

[**KSPROPERTY\_ITD3D\_参数**](ksproperty-itd3d-params.md)

 

 





