---
title: KSMETHOD\_BDA\_启动\_更改
description: 客户端使用 KSMETHOD\_BDA\_启动\_更改以重置更改列表。
ms.assetid: 657fb89d-f216-4352-87d8-3d2d933cc8a5
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
ms.openlocfilehash: 8d056b527c1d60447cfd2fe01514c46d0bc4b757
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842417"
---
# <a name="ksmethod_bda_start_changes"></a>KSMETHOD\_BDA\_启动\_更改


客户端使用 KSMETHOD\_BDA\_启动\_更改以重置更改列表。

## <span id="ddk_ksmethod_bda_start_changes_ks"></span><span id="DDK_KSMETHOD_BDA_START_CHANGES_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

**标记**成员设置为 KSMETHOD 的 KSMETHOD\_类型\_NONE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

在网络提供商开始进行更改之前，它会使 KSMETHOD\_BDA\_启动\_更改请求，这将导致尚未提交的任何现有更改列表被放弃，并通知筛选器的 pin 和节点开始保留跟踪一组新的更改。 然后，网络提供程序在筛选器或其插针上调用必要的接口方法，但实际并未调用这些方法。 如果网络提供程序确定更改不起作用，则可以调用此方法来清除列表。

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


[**BdaStartChanges**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdastartchanges)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

 

 






