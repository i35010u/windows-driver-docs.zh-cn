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
ms.openlocfilehash: 948ab29d0a5e2b41dd267969ca71c21a902f387b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837962"
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
返回时，将包含一个 WMI 限定符值，该值指示操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**GetFCPStatistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_out)结构的**HBAStatus**成员中返回此信息。

*ScsiId*   
返回时，包含[**HBAScsiID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_hbascsiid)类型的结构，该结构保存标识设备的信息。 此信息将传送到结构中[**GetFCPStatistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_in)的**ScsiId**成员中的微型端口驱动程序。

*FC4Statistics*   
返回时，包含一个类型为[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)的结构，该结构保存指示的 SCSI 逻辑单元的统计信息。 微型端口驱动程序在[**GetFCPStatistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_out)结构的**FC4Statistics**成员中返回此信息。

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


[**GetFCPStatistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_in)

[**GetFCPStatistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfcpstatistics_out)

[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

 

 






