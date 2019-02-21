---
title: KSPROPSETID\_BdaPIDFilter
description: KSPROPSETID\_BdaPIDFilter
ms.assetid: 9a2655cb-d7e9-4f61-803a-63fe3fd3501b
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea85c0951b86dc4dbd79844ce3043acd164a1711
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522852"
---
# <a name="kspropsetidbdapidfilter"></a>KSPROPSETID\_BdaPIDFilter


## <span id="ddk_kspropsetid_bdapidfilter_ks"></span><span id="DDK_KSPROPSETID_BDAPIDFILTER_KS"></span>


KSPROPSETID\_BdaPIDFilter 是 BDA 数据包标识符 (PID) 筛选器属性集。 它用于筛选出不需要子流从接收到广播 MPEG2 传输流。 此属性设置控件的 PID 筛选器节点属性。

可用属性如下：

<span id="KSPROPERTY_BDA_PIDFILTER_MAP_PIDS"></span><span id="ksproperty_bda_pidfilter_map_pids"></span>[**KSPROPERTY\_BDA\_PIDFILTER\_MAP\_PIDS**](ksproperty-bda-pidfilter-map-pids.md)  
MPEG2 Pid 的传输流数据包的应传递到下游的筛选器或节点的列表会告知 PID 筛选器节点。

<span id="KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS"></span><span id="ksproperty_bda_pidfilter_unmap_pids"></span>[**KSPROPERTY\_BDA\_PIDFILTER\_UNMAP\_PIDS**](ksproperty-bda-pidfilter-unmap-pids.md)  
标识与特定的 Pid 来筛选从输入流的数据包会告知 PID 筛选器节点。

<span id="KSPROPERTY_BDA_PIDFILTER_LIST_PIDS"></span><span id="ksproperty_bda_pidfilter_list_pids"></span>[**KSPROPERTY\_BDA\_PIDFILTER\_LIST\_PIDS**](ksproperty-bda-pidfilter-list-pids.md)  
返回一个数组标识的 PID 筛选器节点从输入流传递到输出流的数据包的组的 Pid。

 

 





