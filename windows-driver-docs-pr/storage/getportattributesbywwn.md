---
title: GetPortAttributesByWWN 函数
description: GetPortAttributesByWWN 方法检索端口名称指定的端口属性。
ms.assetid: 24b62b1c-9f47-40f1-aa72-849fabcbfbae
keywords:
- GetPortAttributesByWWN 函数存储设备
topic_type:
- apiref
api_name:
- GetPortAttributesByWWN
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d95f9a4fa21a20db7a94bc1a66f1e286c945559
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193203"
---
# <a name="getportattributesbywwn-function"></a>GetPortAttributesByWWN 函数


**GetPortAttributesByWWN**方法检索端口名称指定的端口属性。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetPortAttributesByWWN(
   [in, HBAType("HBA_WWN")] uint8                                     wwn[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                            HBAStatus,
   [out, HBAType("HBA_PORTATTRIBUTES")] MSFC_HBAPortAttributesResults PortAttributes
);
```

<a name="parameters"></a>参数
----------

*wwn \[ 8\]*   
要查询其属性的端口的名称。 此信息将传送到 GetPortAttributesByWWN 结构中的 **wwn** 成员的微型端口 [**驱动 \_ **](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getportattributesbywwn_in) 程序。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**GetPortAttributesByWWN \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getportattributesbywwn_out)结构的**HBAStatus**成员中返回此信息。

*PortAttributes*   
[**MSFC \_ HBAPortAttributesResults**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)类型的结构，可在其中返回发现的 FC \_ 端口的特性。 微型端口驱动程序在[**GetDiscoveredPortAttributes \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)结构的**PortAttributes**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>注解
-------

此 WMI 方法属于 [MSFC \_ HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetPortAttributesByWWN \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getportattributesbywwn_in)

[**GetPortAttributesByWWN \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getportattributesbywwn_out)

[**MSFC \_ HBAPortAttributesResults**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)

 

