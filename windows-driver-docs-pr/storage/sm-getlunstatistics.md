---
title: SM\_GetLUNStatistics 函数
description: SMHBA\_GetLUNStatistics 方法返回特定 SCSI 逻辑单元的流量统计信息，该逻辑单元是使用 FCP 协议或特定本地 HBA 上的 SSP 协议提供的。
ms.assetid: c4e85c59-8b8d-4b68-9ab7-adf1e12fc50c
keywords:
- SM_GetLUNStatistics 函数存储设备
topic_type:
- apiref
api_name:
- SM_GetLUNStatistics
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 040ae128405d41e6f00a769819ec072098afc327
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845486"
---
# <a name="sm_getlunstatistics-function"></a>SM\_GetLUNStatistics 函数


SMHBA\_GetLUNStatistics 方法返回特定 SCSI 逻辑单元的流量统计信息，该逻辑单元是使用 FCP 协议或特定本地 HBA 上的 SSP 协议提供的。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_GetLUNStatistics(
   [in, HBAType("HBA_SCSIID")] HBAScsiID                                     Lunit,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                                   HBAStatus,
   [out, HBAType("MS_SMHBA_PROTOCOLSTATISTICS")] MS_SMHBA_PROTOCOLSTATISTICS ProtocolStatistics
);
```

<a name="parameters"></a>参数
----------

*Lunit*   
类型为[**HBA\_ScsiId**](https://msdn.microsoft.com/library/windows/hardware/ff557191)的结构，其中包含操作系统用于标识 SCSI 逻辑单元的信息。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SM\_GetLUNStatistics\_OUT 结构的 HBAStatus 成员中返回此信息。

*ProtocolStatistics*   
类型为[**MS\_SMHBA\_PROTOCOLSTATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_protocolstatistics)的结构，用于报告端口上的协议流量统计信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_TargetInformationMethods WMI 类。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_GetLUNStatistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getlunstatistics_in)

[**SM\_GetLUNStatistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_getlunstatistics_out)

 

 






