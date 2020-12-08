---
title: KSMETHOD \_ BDA \_ 开始 \_ 更改
description: 客户端使用 KSMETHOD \_ BDA \_ 开始 \_ 更改来重置更改列表。
keywords:
- KSMETHOD_BDA_START_CHANGES 流媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_START_CHANGES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b83c6daad8c205e611f9cf54b78d67d92505a56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836653"
---
# <a name="ksmethod_bda_start_changes"></a>KSMETHOD \_ BDA \_ 开始 \_ 更改


客户端使用 KSMETHOD \_ BDA \_ 开始 \_ 更改来重置更改列表。

## <span id="ddk_ksmethod_bda_start_changes_ks"></span><span id="DDK_KSMETHOD_BDA_START_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

**标记** 成员设置为 KSMETHOD 的 KSMETHOD \_ \_ 。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

在网络提供商开始进行更改之前，它会生成一个 KSMETHOD 的 \_ BDA \_ START \_ change 请求，这将导致尚未提交的任何现有更改列表被放弃，并通知筛选器的 pin 和节点开始跟踪一组新的更改。 然后，网络提供程序在筛选器或其插针上调用必要的接口方法，但实际并未调用这些方法。 如果网络提供程序确定更改不起作用，则可以调用此方法来清除列表。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**BdaStartChanges**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdastartchanges)

[**KSMETHOD**](/previous-versions/ff563398(v=vs.85))

 

