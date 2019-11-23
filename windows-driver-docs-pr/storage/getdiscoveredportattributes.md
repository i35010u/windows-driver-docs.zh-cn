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
ms.openlocfilehash: 2ae58ad5bd0bbf7649f5d7858ae9f1268eb4a9ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837848"
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
类型为 Nx 的本地端口的索引\_端口，通过该端口查询发现的远程端口。 此信息将传送到结构中[**GetDiscoveredPortAttributes\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)的**PortIndex**成员中的微型端口驱动程序。

*DiscoveredPortIndex*   
要查询的远程端口的索引。 此信息将传送到结构中[**GetDiscoveredPortAttributes\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)的**DiscoveredPortIndex**成员中的微型端口驱动程序。

*HBAStatus*   
返回时，将包含一个 WMI 限定符值，该值指示操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**GetDiscoveredPortAttributes\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)结构的**HBAStatus**成员中返回此信息。

*PortAttributes*   
类型为[**MSFC\_HBAPortAttributesResults**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)的结构，可在其中返回发现的 FC\_端口的特性。 微型端口驱动程序在[**GetDiscoveredPortAttributes\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)结构的**PortAttributes**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_HBAADAPTERMETHODS WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi （包括 Hbapiwmi、Hbaapi 或 Hbaapi）。</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetDiscoveredPortAttributes\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_in)

[**GetDiscoveredPortAttributes\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getdiscoveredportattributes_out)

[**MSFC\_HBAPortAttributesResults**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_hbaportattributesresults)

 

 






