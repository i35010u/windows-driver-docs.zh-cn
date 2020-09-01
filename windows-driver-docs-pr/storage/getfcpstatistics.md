---
title: GetFCPStatistics 函数
description: GetFCPStatistics WMI 方法返回指定的本地 HBA 上所指示的 SCSI 逻辑单元的 FCP 流量统计信息。
ms.assetid: 566368d7-ee13-449d-97c3-1c214984fee5
keywords:
- GetFCPStatistics 函数存储设备
topic_type:
- apiref
api_name:
- GetFCPStatistics
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: acf5a24aca9351c6e8e896f4a502f149632d1f21
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191157"
---
# <a name="getfcpstatistics-function"></a>GetFCPStatistics 函数


**GetFCPStatistics** WMI 方法返回指定的本地 HBA 上所指示的 SCSI 逻辑单元的 FCP 流量统计信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFCPStatistics(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in] HBAScsiID                          ScsiId,
   [out] MSFC_FC4STATISTICS                FC4Statistics
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，将包含一个 WMI 限定符值，该值指示操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**GetFCPStatistics \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_out)结构的**HBAStatus**成员中返回此信息。

*ScsiId*   
返回时，包含 [**HBAScsiID**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid) 类型的结构，该结构保存标识设备的信息。 此信息将传送到结构[** \_ 中 GetFCPStatistics**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_in)的**ScsiId**成员中的微型端口驱动程序。

*FC4Statistics*   
返回时，包含 [**MSFC \_ FC4STATISTICS**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics) 类型的结构，该结构保存指示的 SCSI 逻辑单元的统计信息。 微型端口驱动程序在[**GetFCPStatistics \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_out)结构的**FC4Statistics**成员中返回此信息。

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


[**GetFCPStatistics \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_in)

[**GetFCPStatistics \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_out)

[**MSFC \_ FC4STATISTICS**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

 

