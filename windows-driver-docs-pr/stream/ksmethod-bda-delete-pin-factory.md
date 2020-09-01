---
title: KSMETHOD \_ BDA \_ 删除 \_ PIN \_ 工厂
description: 客户端使用 KSMETHOD \_ BDA \_ delete \_ PIN \_ 工厂删除用于筛选器的 PIN 工厂。
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
ms.openlocfilehash: 33b83b7a25d72eeaba4906e2efdd12128a665658
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192175"
---
# <a name="ksmethod_bda_delete_pin_factory"></a>KSMETHOD \_ BDA \_ 删除 \_ PIN \_ 工厂


客户端使用 KSMETHOD \_ BDA \_ delete \_ PIN \_ 工厂删除用于筛选器的 PIN 工厂。

## <span id="ddk_ksmethod_bda_delete_pin_factory_ks"></span><span id="DDK_KSMETHOD_BDA_DELETE_PIN_FACTORY_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

KSM \_ PIN，并将**方法**成员的**FLAGS**成员设置为 KSMETHOD \_ 类型 \_ NONE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

无

<a name="remarks"></a>备注
-------

指定要在 KSM pin 结构的 **PinId** 成员中删除的 pin 工厂 \_ 。

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


[**BdaMethodDeletePin**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethoddeletepin)

[**KSM \_ PIN**](/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_ksm_pin)

 

