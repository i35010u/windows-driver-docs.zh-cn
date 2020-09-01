---
title: GetDiscoveredPortAttributes 函数
description: GetDiscoveredPortAttributes WMI 方法检索指定远程光纤通道端口的属性。
ms.assetid: f71a02cf-035a-4de2-bb28-e1141a92795c
keywords:
- GetDiscoveredPortAttributes 函数存储设备
topic_type:
- apiref
api_name:
- GetDiscoveredPortAttributes
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49c82ce1f9fe49789817f5b93702b933cc1894bc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185451"
---
# <a name="getdiscoveredportattributes-function"></a>GetDiscoveredPortAttributes 函数


**GetDiscoveredPortAttributes** WMI 方法检索指定远程光纤通道端口的属性。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetDiscoveredPortAttributes(
   [in] uint32                                                        PortIndex,
   [in] uint32                                                        DiscoveredPortIndex,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                            HBAStatus,
   [out, HBAType("HBA_PORTATTRIBUTES")] MSFC_HBAPortAttributesResults PortAttributes
);
```

<a name="parameters"></a>参数
----------

*PortIndex*   
\_用于查询发现的远程端口的 Nx 端口类型的本地端口的索引。 此信息将传送到结构[** \_ 中 GetDiscoveredPortAttributes**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)的**PortIndex**成员中的微型端口驱动程序。

*DiscoveredPortIndex*   
要查询的远程端口的索引。 此信息将传送到结构[** \_ 中 GetDiscoveredPortAttributes**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)的**DiscoveredPortIndex**成员中的微型端口驱动程序。

*HBAStatus*   
返回时，将包含一个 WMI 限定符值，该值指示操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**GetDiscoveredPortAttributes \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)结构的**HBAStatus**成员中返回此信息。

*PortAttributes*   
[**MSFC \_ HBAPortAttributesResults**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)类型的结构，可在其中返回发现的 FC \_ 端口的特性。 微型端口驱动程序在[**GetDiscoveredPortAttributes \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)结构的**PortAttributes**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
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
<td align="left">“桌面”</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetDiscoveredPortAttributes \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)

[**GetDiscoveredPortAttributes \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)

[**MSFC \_ HBAPortAttributesResults**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)

 

