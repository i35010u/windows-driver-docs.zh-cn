---
title: KSMETHOD\_BDA\_获取\_更改\_状态
description: 客户端使用 KSMETHOD\_BDA\_获取\_更改\_状态，以确定筛选器的当前更改状态。
ms.assetid: bb635b88-6d51-4d0c-9134-2fc6287a4146
keywords:
- KSMETHOD_BDA_GET_CHANGE_STATE 流式处理媒体设备
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
ms.openlocfilehash: f85096e8d1605cda1e30efdba0ef7d8abedc4e99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362635"
---
# <a name="ksmethodbdagetchangestate"></a>KSMETHOD\_BDA\_获取\_更改\_状态


客户端使用 KSMETHOD\_BDA\_获取\_更改\_状态，以确定筛选器的当前更改状态。

## <span id="ddk_ksmethod_bda_get_change_state_ks"></span><span id="DDK_KSMETHOD_BDA_GET_CHANGE_STATE_KS"></span>


### <a name="span-idspecifyingthismethodspanspan-idspecifyingthismethodspanspan-idspecifyingthismethodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

使用 KSMETHOD**标志**成员设置为 KSMETHOD\_类型\_读取。

### <a name="span-idmethoddataspanspan-idmethoddataspanspan-idmethoddataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

值从 BDA\_更改\_标识当前的状态枚举类型更改为筛选器的状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**BDA\_更改\_状态**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556518(v=vs.85))

[**BdaGetChangeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdagetchangestate)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

 

 






