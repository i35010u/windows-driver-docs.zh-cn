---
title: KSMETHOD \_ BDA \_ 提交 \_ 更改
description: 客户端使用 KSMETHOD \_ BDA \_ 提交 \_ 更改来提交请求的更改列表。
ms.assetid: f6572a4e-2328-4157-80f7-110e0fe58a4f
keywords:
- KSMETHOD_BDA_COMMIT_CHANGES 流媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_COMMIT_CHANGES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0615525c204a7f561f1a40f36f7d4c661cc1e6ad
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188177"
---
# <a name="ksmethod_bda_commit_changes"></a>KSMETHOD \_ BDA \_ 提交 \_ 更改


客户端使用 KSMETHOD \_ BDA \_ 提交 \_ 更改来提交请求的更改列表。

## <span id="ddk_ksmethod_bda_commit_changes_ks"></span><span id="DDK_KSMETHOD_BDA_COMMIT_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

**标记**成员设置为 KSMETHOD 的 KSMETHOD \_ \_ 。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

当网络提供程序发出 KSMETHOD \_ BDA \_ COMMIT \_ 更改请求时，将在基础筛选器上提交更改列表，此时筛选器将重置其状态，并开始新的循环。

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


[**BdaCommitChanges**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacommitchanges)

[**KSMETHOD**](/previous-versions/ff563398(v=vs.85))

 

