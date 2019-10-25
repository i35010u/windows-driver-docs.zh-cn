---
title: KSMETHOD\_BDA\_删除\_PIN\_工厂
description: 客户端使用 KSMETHOD\_BDA\_删除\_PIN\_工厂删除用于筛选器的 pin 工厂。
ms.assetid: b9e9306a-5b0e-47d0-9194-eb60d793bebc
keywords:
- KSMETHOD_BDA_DELETE_PIN_FACTORY 流媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_DELETE_PIN_FACTORY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89433126fc2655dc588170abcd94987b6a54c5d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842420"
---
# <a name="ksmethod_bda_delete_pin_factory"></a>KSMETHOD\_BDA\_删除\_PIN\_工厂


客户端使用 KSMETHOD\_BDA\_删除\_PIN\_工厂删除用于筛选器的 pin 工厂。

## <span id="ddk_ksmethod_bda_delete_pin_factory_ks"></span><span id="DDK_KSMETHOD_BDA_DELETE_PIN_FACTORY_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

KSM\_将**方法**成员的**Flags**成员设置为 KSMETHOD\_类型\_NONE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

指定要在 KSM\_固定结构的**PinId**成员中删除的 pin 工厂。

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


[**BdaMethodDeletePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethoddeletepin)

[**KSM\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_ksm_pin)

 

 






