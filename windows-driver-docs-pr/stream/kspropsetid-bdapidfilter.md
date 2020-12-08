---
title: KSPROPSETID \_ BdaPIDFilter
description: KSPROPSETID \_ BdaPIDFilter
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 557b6150515c634a71b40250366a99b89a2dfa5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837837"
---
# <a name="kspropsetid_bdapidfilter"></a>KSPROPSETID \_ BdaPIDFilter


## <span id="ddk_kspropsetid_bdapidfilter_ks"></span><span id="DDK_KSPROPSETID_BDAPIDFILTER_KS"></span>


KSPROPSETID \_ BdaPIDFilter 是 (PID) filter 属性集的 BDA 数据包标识符。 它用于从收到的广播 MPEG2 传输流中筛选出不需要的 substreams。 此属性集控制 PID 筛选器节点的属性。

以下属性可用：

<span id="KSPROPERTY_BDA_PIDFILTER_MAP_PIDS"></span><span id="ksproperty_bda_pidfilter_map_pids"></span>[**KSPROPERTY \_ BDA \_ PIDFILTER \_ 映射 \_ PID**](ksproperty-bda-pidfilter-map-pids.md)  
通知 PID 筛选器节点有关应传递到下游筛选器或节点的传输流包的 MPEG2 Pid 列表。

<span id="KSPROPERTY_BDA_PIDFILTER_UNMAP_PIDS"></span><span id="ksproperty_bda_pidfilter_unmap_pids"></span>[**KSPROPERTY \_ BDA \_ PIDFILTER 取消 \_ 映射 \_ PID**](ksproperty-bda-pidfilter-unmap-pids.md)  
通知 PID 筛选器节点有关用特定 Pid 标识的数据包，以便从输入流进行筛选。

<span id="KSPROPERTY_BDA_PIDFILTER_LIST_PIDS"></span><span id="ksproperty_bda_pidfilter_list_pids"></span>[**KSPROPERTY \_ BDA \_ PIDFILTER \_ 列表 \_ PID**](ksproperty-bda-pidfilter-list-pids.md)  
返回一个 Pid 数组，该数组标识 PID 筛选器节点从输入流传递到输出流的数据包组。

 

 





