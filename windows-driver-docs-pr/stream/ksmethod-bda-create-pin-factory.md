---
title: KSMETHOD \_ BDA \_ 创建 \_ PIN \_ 工厂
description: 客户端使用 KSMETHOD \_ BDA \_ create \_ PIN \_ 工厂创建用于筛选器的 PIN 工厂。
keywords:
- KSMETHOD_BDA_CREATE_PIN_FACTORY 流媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_CREATE_PIN_FACTORY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50eb10b34ec5612a21728fd4a8134ae799499bed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824941"
---
# <a name="ksmethod_bda_create_pin_factory"></a>KSMETHOD \_ BDA \_ 创建 \_ PIN \_ 工厂


客户端使用 KSMETHOD \_ BDA \_ create \_ PIN \_ 工厂创建用于筛选器的 PIN 工厂。

## <span id="ddk_ksmethod_bda_create_pin_factory_ks"></span><span id="DDK_KSMETHOD_BDA_CREATE_PIN_FACTORY_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

KSM \_ PIN，并将 **方法** 成员的 **FLAGS** 成员设置为 KSMETHOD \_ 类型 \_ READ。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

ULONG，表示 pin 工厂的标识符。

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


[**BdaMethodCreatePin**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethodcreatepin)

[**KSM \_ PIN**](/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_ksm_pin)

 

