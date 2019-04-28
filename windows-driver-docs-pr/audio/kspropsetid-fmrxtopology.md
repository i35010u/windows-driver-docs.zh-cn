---
title: KSPROPSETID\_FMRXTopology
description: KSPROPSETID\_FMRXTopology 属性集用于设置 FM 单选属性。
ms.assetid: 66ACE82D-F0C2-4BF8-9B16-8A1B3A2C05E0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5adc0f31ca156727332ec9664cda43ef8ef7e98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332487"
---
# <a name="kspropsetidfmrxtopology"></a>KSPROPSETID\_FMRXTopology


`KSPROPSETID_FMRXTopology`属性集用于设置 FM 单选属性。

`KSPROPSETID_FMRXTopology`属性集包含以下属性：

-   [**KSPROPERTY\_FMRX\_ANTENNAENDPOINTID**](ksproperty-fmrx-antennaendpointid.md)

-   [**KSPROPERTY\_FMRX\_ENDPOINTID**](ksproperty-fmrx-endpointid.md)

-   [**KSPROPERTY\_FMRX\_VOLUME**](ksproperty-fmrx-volume.md)

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


可以启用或禁用通过设置调频广播[ **KSPROPERTY\_FMRX\_状态**](ksproperty-fmrx-state.md)批筛选器的属性。 FM 卷和路由 （终结点选择） 受[ **KSPROPERTY\_FMRX\_卷**](ksproperty-fmrx-volume.md)并[ **KSPROPERTY\_FMRX\_ENDPOINTID** ](ksproperty-fmrx-endpointid.md)拓扑筛选器的属性。 对的基本支持**KSPROPERTY\_FMRX\_卷**属性应返回最小的卷、 最大卷和卷范围。

一个新[ **KSNODETYPE\_FM\_RX** ](ksnodetype-fm-rx.md)拓扑节点终结点实现如任何其他音频的终结点是在系统中，并支持音频终结点的所有属性。 此终结点还支持下定义的插孔属性[KSPROPSETID\_Jack](kspropsetid-jack.md)属性集。 此终结点是在启动时拔出状态。 如果驱动程序支持捕获调频广播，此终结点变为活动状态时启用了 FM 收音机中。 创建一个捕获固定**KSNODETYPE\_FM\_RX**拓扑节点允许来自 FM 接收方的音频捕获。

 

 





