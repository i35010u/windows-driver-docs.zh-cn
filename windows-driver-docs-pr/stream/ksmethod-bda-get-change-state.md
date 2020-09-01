---
title: KSMETHOD \_ BDA \_ 获取 \_ 更改 \_ 状态
description: 客户端使用 KSMETHOD \_ BDA \_ GET \_ CHANGE \_ 状态来确定筛选器的当前更改状态。
ms.assetid: bb635b88-6d51-4d0c-9134-2fc6287a4146
keywords:
- KSMETHOD_BDA_GET_CHANGE_STATE 流媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_GET_CHANGE_STATE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42ea045b2922db858df66b672a1543dbdc96fec4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192169"
---
# <a name="ksmethod_bda_get_change_state"></a>KSMETHOD \_ BDA \_ 获取 \_ 更改 \_ 状态


客户端使用 KSMETHOD \_ BDA \_ GET \_ CHANGE \_ 状态来确定筛选器的当前更改状态。

## <span id="ddk_ksmethod_bda_get_change_state_ks"></span><span id="DDK_KSMETHOD_BDA_GET_CHANGE_STATE_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

KSMETHOD，其 **Flags** 成员设置为 KSMETHOD \_ 类型 \_ READ。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

\_ \_ 用于标识筛选器当前更改状态的 "BDA 更改状态" 枚举类型的值。

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

## <a name="see-also"></a>另请参阅


[**BDA \_ 更改 \_ 状态**](/previous-versions/windows/hardware/drivers/ff556518(v=vs.85))

[**BdaGetChangeState**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdagetchangestate)

[**KSMETHOD**](/previous-versions/ff563398(v=vs.85))

 

