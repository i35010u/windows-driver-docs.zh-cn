---
title: KSMETHOD\_BDA\_检查\_更改
description: 客户端使用 KSMETHOD\_BDA\_检查\_更改以确定请求的更改列表是否有效。
ms.assetid: 00a2d0ca-0ede-4ae5-ab2a-95d19143ea7c
keywords:
- KSMETHOD_BDA_CHECK_CHANGES 流媒体设备
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
ms.openlocfilehash: 0579adf7ddda38b0294aa4f90a4e4d427f9794a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838864"
---
# <a name="ksmethod_bda_check_changes"></a>KSMETHOD\_BDA\_检查\_更改


客户端使用 KSMETHOD\_BDA\_检查\_更改以确定请求的更改列表是否有效。

## <span id="ddk_ksmethod_bda_check_changes_ks"></span><span id="DDK_KSMETHOD_BDA_CHECK_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

**标记**成员设置为 KSMETHOD 的 KSMETHOD\_类型\_NONE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

提交更改列表之前，网络提供程序会\_BDA\_检查\_更改请求，以确定所请求的更改是否有效。 在发出此请求时，微型驱动程序可以保留资源，以确保资源可用。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BdaCheckChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacheckchanges)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

 

 






