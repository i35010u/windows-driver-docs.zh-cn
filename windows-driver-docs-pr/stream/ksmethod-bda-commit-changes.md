---
title: KSMETHOD\_BDA\_提交\_更改
description: 客户端使用 KSMETHOD\_BDA\_提交\_更改，以提交请求的更改列表。
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
ms.openlocfilehash: ab1034a16c59a519b7d45fffad1fdd8220674eca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842427"
---
# <a name="ksmethod_bda_commit_changes"></a>KSMETHOD\_BDA\_提交\_更改


客户端使用 KSMETHOD\_BDA\_提交\_更改，以提交请求的更改列表。

## <span id="ddk_ksmethod_bda_commit_changes_ks"></span><span id="DDK_KSMETHOD_BDA_COMMIT_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

**标记**成员设置为 KSMETHOD 的 KSMETHOD\_类型\_NONE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

当网络提供商\_BDA\_提交\_更改请求时，将在基础筛选器上提交更改列表，此时筛选器将重置其状态，并开始新的循环。

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


[**BdaCommitChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdacommitchanges)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

 

 






