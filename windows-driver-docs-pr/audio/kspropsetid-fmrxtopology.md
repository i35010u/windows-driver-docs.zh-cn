---
title: KSPROPSETID \_ FMRXTopology
description: KSPROPSETID \_ FMRXTopology 属性集用于设置调频单选属性。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: acae9ce106502342975f377fc3671455cf729269
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801089"
---
# <a name="kspropsetid_fmrxtopology"></a>KSPROPSETID \_ FMRXTopology


`KSPROPSETID_FMRXTopology`属性集用于设置调频单选属性。

`KSPROPSETID_FMRXTopology`属性集包括以下属性：

-   [**KSPROPERTY \_ FMRX \_ ANTENNAENDPOINTID**](ksproperty-fmrx-antennaendpointid.md)

-   [**KSPROPERTY \_ FMRX \_ ENDPOINTID**](ksproperty-fmrx-endpointid.md)

-   [**KSPROPERTY \_ FMRX \_**](ksproperty-fmrx-volume.md)

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


可以通过在 wave 滤镜上设置 [**KSPROPERTY \_ FMRX \_ STATE**](ksproperty-fmrx-state.md) 属性来启用或禁用调频广播。 FM volume 和路由 (终结点选择) 由拓扑筛选器上的 [**KSPROPERTY \_ FMRX \_ volume**](ksproperty-fmrx-volume.md) 和 [**KSPROPERTY \_ FMRX \_ ENDPOINTID**](ksproperty-fmrx-endpointid.md) 属性控制。 **KSPROPERTY \_ FMRX \_ volume** 属性的基本支持应返回最小卷、最大卷和卷范围。

新的 [**KSNODETYPE \_ FM \_ RX**](ksnodetype-fm-rx.md) 拓扑节点终结点实现为系统中的任何其他音频终结点，并且它支持所有音频终结点属性。 此终结点还支持在 [KSPROPSETID \_ 插座](kspropsetid-jack.md) 属性集下定义的插座属性。 此终结点在启动时处于拔出状态。 如果驱动程序支持捕获调频广播，则启用调频广播后，此终结点将变为活动状态。 在 **KSNODETYPE \_ FM \_ RX** 拓扑节点上创建捕获 pin 后，可通过调频接收机接收音频捕获。

 

 





