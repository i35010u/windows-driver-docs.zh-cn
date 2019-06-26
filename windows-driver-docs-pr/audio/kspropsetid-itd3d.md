---
title: KSPROPSETID\_Itd3d
description: KSPROPSETID\_Itd3d
ms.assetid: 87159be4-740e-47c9-b16f-16ca4d01c793
keywords:
- KSPROPSETID_Itd3d
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37fd00ff53ffde7064dd8f447fbcd281b8a0d9a1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360487"
---
# <a name="kspropsetiditd3d"></a>KSPROPSETID\_Itd3d


## <span id="ddk_kspropsetid_itd3d_ks"></span><span id="DDK_KSPROPSETID_ITD3D_KS"></span>


`KSPROPSETID_Itd3d`属性设置用于配置使用 3D 节点的 interaural 时间延迟 (ITD) 算法 ([**KSNODETYPE\_3D\_效果**](ksnodetype-3d-effects.md))。

达到侦听器的声音左边缘和右耳朵从特定的声音源延迟按不同的量，具体取决于源的位置。 侦听器可以推断出的声音差异延迟量来源的方向。 ITD 算法可控制的差异的延迟，以模拟在 3D 空间中的特定位置的声音源。

ITD 算法通过控制的量达到每个 ear 声音 muffled 依据提供额外的声音定位的提示。 高频率声音可以 muffled 来模拟声音源位于该侦听器的头。 对于附近右 ear 声音源，例如，达到左的 ear 的声音是更 muffled 比到达正确清除。 将从一些比例中的声音源的原始信号与低通筛选版本相同的信号相结合，可生成 muffled 的声音。 衰减原始信号时增加从低通贡献筛选版本模拟移动的模拟声音源进一步侦听器的 head 后的效果。

声音源的位置更改时，必须更新以下参数：

-   达到每个 ear 声音中的延迟量。

-   达到每个 ear 声音 muffled 依据量。

点击量和其他虚假的噪声，可能会导致对这些参数进行即时更改。 为了筛选出此类噪音的示例在大量这些参数中的 ITD 算法平滑处理，从而转换。

有关使用 ITD 算法的参数的详细信息，请参阅[ **KSDS3D\_ITD\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksds3d_itd_params)。

设置此属性包含一个属性：

[**KSPROPERTY\_ITD3D\_PARAMS**](ksproperty-itd3d-params.md)

 

 





