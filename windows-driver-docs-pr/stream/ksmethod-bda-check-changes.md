---
title: KSMETHOD\_BDA\_检查\_更改
description: 客户端使用 KSMETHOD\_BDA\_检查\_更改，以确定是否起作用的请求的更改列表。
ms.assetid: 00a2d0ca-0ede-4ae5-ab2a-95d19143ea7c
keywords:
- KSMETHOD_BDA_CHECK_CHANGES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_CHECK_CHANGES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0bd12054bc7370d39965d9f34323f6c0e588956
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567696"
---
# <a name="ksmethodbdacheckchanges"></a>KSMETHOD\_BDA\_检查\_更改


客户端使用 KSMETHOD\_BDA\_检查\_更改，以确定是否起作用的请求的更改列表。

## <span id="ddk_ksmethod_bda_check_changes_ks"></span><span id="DDK_KSMETHOD_BDA_CHECK_CHANGES_KS"></span>


### <a name="span-idspecifyingthismethodspanspan-idspecifyingthismethodspanspan-idspecifyingthismethodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

使用 KSMETHOD**标志**成员设置为 KSMETHOD\_类型\_NONE。

### <a name="span-idmethoddataspanspan-idmethoddataspanspan-idmethoddataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

提交更改的列表之前, 网络提供程序 KSMETHOD\_BDA\_检查\_更改请求，以确定请求的更改是否起作用。 微型驱动程序可能会发出此请求后，以确保有足够的资源预留资源。

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


[**BdaCheckChanges**](https://msdn.microsoft.com/library/windows/hardware/ff556433)

[**KSMETHOD**](https://msdn.microsoft.com/library/windows/hardware/ff563398)

 

 






