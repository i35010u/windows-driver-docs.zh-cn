---
title: SM\_GetLUNStatistics 函数
description: SMHBA\_GetLUNStatistics 方法将返回一个特定的 SCSI 逻辑单元，通过在特定的本地 HBA 上使用 FCP 协议或 SSP 协议提供的流量统计数据。
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
ms.openlocfilehash: fb6e6fa06c220b001f993fa8b4416e2afa27d77e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384314"
---
# <a name="smgetlunstatistics-function"></a>SM\_GetLUNStatistics 函数


SMHBA\_GetLUNStatistics 方法将返回一个特定的 SCSI 逻辑单元，通过在特定的本地 HBA 上使用 FCP 协议或 SSP 协议提供的流量统计数据。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_GetLUNStatistics(
   [in, HBAType("HBA_SCSIID")] HBAScsiID                                     Lunit,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                                   HBAStatus,
   [out, HBAType("MS_SMHBA_PROTOCOLSTATISTICS")] MS_SMHBA_PROTOCOLSTATISTICS ProtocolStatistics
);
```

<a name="parameters"></a>Parameters
----------

*Lunit*   
类型的结构[ **HBA\_ScsiId** ](https://msdn.microsoft.com/library/windows/hardware/ff557191) ，包含操作系统用于标识 SCSI 逻辑单元的信息。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_GetLUNStatistics\_结构。

*ProtocolStatistics*   
类型的结构[ **MS\_SMHBA\_PROTOCOLSTATISTICS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_protocolstatistics)用于报表的端口上的协议流量统计信息。

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
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_GetLUNStatistics\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_getlunstatistics_in)

[**SM\_GetLUNStatistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_getlunstatistics_out)

 

 






