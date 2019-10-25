---
title: KSMETHOD\_BDA\_创建\_PIN\_工厂
description: 客户端使用 KSMETHOD\_BDA\_创建\_PIN\_工厂创建用于筛选器的 pin 工厂。
ms.assetid: ebc9dc1d-1b4b-40d3-82b5-f32d3781537c
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
ms.openlocfilehash: 5687a4d3cd8d8d58b488571ef5abed3cd9c7c6a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842424"
---
# <a name="ksmethod_bda_create_pin_factory"></a>KSMETHOD\_BDA\_创建\_PIN\_工厂


客户端使用 KSMETHOD\_BDA\_创建\_PIN\_工厂创建用于筛选器的 pin 工厂。

## <span id="ddk_ksmethod_bda_create_pin_factory_ks"></span><span id="DDK_KSMETHOD_BDA_CREATE_PIN_FACTORY_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

KSM\_PIN，并将**方法**成员的**Flags**成员设置为 KSMETHOD\_类型\_READ。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BdaMethodCreatePin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethodcreatepin)

[**KSM\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_ksm_pin)

 

 






