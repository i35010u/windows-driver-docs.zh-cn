---
title: GetFcpTargetMapping 函数
description: GetFcpTargetMapping WMI 方法检索用于唯一标识操作系统的一组逻辑单元的信息与这些逻辑单元的光纤通道协议 (FCP) 标识符之间的映射。
ms.assetid: 2e4b3554-31de-4eaa-9228-844639a219d5
keywords:
- GetFcpTargetMapping 函数存储设备
topic_type:
- apiref
api_name:
- GetFcpTargetMapping
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f6a8fdd12981a146dab95d2c61d2a508240d2aaa
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188829"
---
# <a name="getfcptargetmapping-function"></a>GetFcpTargetMapping 函数


**GetFcpTargetMapping** WMI 方法检索用于唯一标识操作系统的一组逻辑单元的信息与这些逻辑单元的光纤通道协议 (FCP) 标识符之间的映射。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFcpTargetMapping(
   [in, HBAType("HBA_WWN")] uint8                    HbaPortWWN[8],
   [in] uint32                                       InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS           HBAStatus,
   [out] uint32                                      TotalEntryCount,
   [out] uint32                                      OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] HBAFCPScsiEntry Entry[]
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN \[ 8\]*   
要检索其映射表的端口的全球名称。 此信息将传送到结构[** \_ 中 GetFcpTargetMapping**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_in)的**HbaPortWWN**成员中的微型端口驱动程序。

*InEntryCount*   
指示 WMI 提供程序可以在 *输入* 参数中报告的绑定项的数目。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**GetFcpTargetMapping \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_out)结构的**HBAStatus**成员中返回此信息。

*TotalEntryCount*   
指示与 HBA 关联的永久性绑定的总数。

*OutEntryCount*   
指示 **GetFcpTargetMapping** 方法检索到的映射总数。 此值将小于或等于 *TotalEntryCount*。

*条目\[\]*   
[**HBAFCPScsiEntry**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbafcpscsientry)类型的结构的数组，这些结构描述了操作系统与光纤通道协议之间的 HBA 绑定 (FCP) 标识符。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 [MSFC \_ HBAFCPInfo WMI 类](msfc-hbafcpinfo-wmi-class.md)。

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


[HBA \_ 状态](hba-status.md)

[**GetFcpTargetMapping \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_in)

[**GetFcpTargetMapping \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_out)

 

