---
title: KSMETHOD \_ BDA \_ 检查 \_ 更改
description: 客户端使用 KSMETHOD \_ BDA \_ 检查 \_ 更改来确定请求的更改列表是否有效。
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
ms.openlocfilehash: 5cfde5d88c89206cae676488c0266e551de3fc77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790205"
---
# <a name="ksmethod_bda_check_changes"></a>KSMETHOD \_ BDA \_ 检查 \_ 更改


客户端使用 KSMETHOD \_ BDA \_ 检查 \_ 更改来确定请求的更改列表是否有效。

## <span id="ddk_ksmethod_bda_check_changes_ks"></span><span id="DDK_KSMETHOD_BDA_CHECK_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

**标记** 成员设置为 KSMETHOD 的 KSMETHOD \_ \_ 。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

提交更改列表之前，网络提供程序会进行 KSMETHOD 的 \_ BDA \_ 检查 \_ 更改请求，以确定所请求的更改是否有效。 在发出此请求时，微型驱动程序可以保留资源，以确保资源可用。

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


[**BdaCheckChanges**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacheckchanges)

[**KSMETHOD**](/previous-versions/ff563398(v=vs.85))

 

