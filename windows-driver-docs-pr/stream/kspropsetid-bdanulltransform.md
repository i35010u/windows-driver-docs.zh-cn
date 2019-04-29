---
title: KSPROPSETID\_BdaNullTransform
description: KSPROPSETID\_BdaNullTransform
ms.assetid: 08277c76-4fa5-46d0-8c86-4bc0e060fa9c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8514f5555bfa1d5a013b360a5cd8bf5c65dd43d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389226"
---
# <a name="kspropsetidbdanulltransform"></a>KSPROPSETID\_BdaNullTransform


## <span id="ddk_kspropsetid_bdanulltransform_ks"></span><span id="DDK_KSPROPSETID_BDANULLTRANSFORM_KS"></span>


KSPROPSETID\_BdaNullTransform 是 BDA **null**转换属性集。 它用于指示要传递通过信号而无需更改的节点。 正在启动**NULL**节点上的转换有效地更改从其输入到其与任何其他函数的输出直接连接到的节点。

可用属性如下：

<span id="KSPROPERTY_BDA_NULL_TRANSFORM_START"></span><span id="ksproperty_bda_null_transform_start"></span>[**KSPROPERTY\_BDA\_NULL\_TRANSFORM\_START**](ksproperty-bda-null-transform-start.md)  
禁用任何转换该节点之前应用于信号，并允许通过该节点的信号不变。

<span id="KSPROPERTY_BDA_NULL_TRANSFORM_STOP"></span><span id="ksproperty_bda_null_transform_stop"></span>[**KSPROPERTY\_BDA\_NULL\_TRANSFORM\_STOP**](ksproperty-bda-null-transform-stop.md)  
重新启动的转换的节点执行了信号之前该转换已禁用与 KSPROPERTY\_BDA\_NULL\_转换\_START 属性。

### <a name="comments"></a>备注

网络提供程序筛选器可以使用此属性集，如果节点支持它并且网络提供程序需要通过该特定节点保持不变的信号。

 

 





