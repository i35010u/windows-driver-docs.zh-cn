---
title: KSPROPSETID \_ BdaNullTransform
description: KSPROPSETID \_ BdaNullTransform
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2601b611a53a76c4c43ad5bd8674f542bc584b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837839"
---
# <a name="kspropsetid_bdanulltransform"></a>KSPROPSETID \_ BdaNullTransform


## <span id="ddk_kspropsetid_bdanulltransform_ks"></span><span id="DDK_KSPROPSETID_BDANULLTRANSFORM_KS"></span>


KSPROPSETID \_ BdaNullTransform 为 BDA **null** 转换属性集。 它用于指示节点通过传递信号而不进行任何更改。 在节点上启动 **NULL** 转换可以有效地将节点从其输入更改为其输出，而无其他功能。

以下属性可用：

<span id="KSPROPERTY_BDA_NULL_TRANSFORM_START"></span><span id="ksproperty_bda_null_transform_start"></span>[**KSPROPERTY \_ BDA \_ NULL \_ 转换 \_ 启动**](ksproperty-bda-null-transform-start.md)  
禁用节点之前应用到信号的任何转换，并允许信号无变化地通过节点。

<span id="KSPROPERTY_BDA_NULL_TRANSFORM_STOP"></span><span id="ksproperty_bda_null_transform_stop"></span>[**KSPROPERTY \_ BDA \_ NULL \_ 转换 \_ 停止**](ksproperty-bda-null-transform-stop.md)  
在已禁用 KSPROPERTY \_ BDA \_ NULL \_ 转换 \_ 启动属性的转换之前，重新启动该转换在信号上执行的转换。

### <a name="comments"></a>注释

如果节点支持该属性，则网络提供程序筛选器可以使用此属性集，网络提供程序需要该信号通过不更改的特定节点。

 

 





