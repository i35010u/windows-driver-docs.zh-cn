---
title: ScsiReportLuns 函数
description: ScsiReportLuns WMI 方法将 SCSI 报表 Lun 命令发送到指定的设备。
ms.assetid: 12c9138d-41b7-404f-8431-08d7cf9cc330
keywords:
- ScsiReportLuns 函数存储设备
topic_type:
- apiref
api_name:
- ScsiReportLuns
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 06e6d6ff0c68162fdeeff9bac8d5d851248c4df8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186647"
---
# <a name="scsireportluns-function"></a>ScsiReportLuns 函数


**ScsiReportLuns** WMI 方法将 SCSI 报表 lun 命令发送到指定的设备。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void ScsiReportLuns(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [in] uint8                                   Cdb[12],
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[8],
   [out] uint32                                 ResponseBufferSize,
   [out] uint32                                 SenseBufferSize,
   [out] uint8                                  ScsiStatus,
   [out, WmiSizeIs("ResponseBufferSize")] uint8 ResponseBuffer[],
   [out, WmiSizeIs("SenseBufferSize")] uint8    SenseBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**ScsiReportLuns \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)结构的**HBAStatus**成员中返回此信息。

*Cdb*   
包含要发送到目标设备的 SCSI 报表 Lun 命令的命令描述符块。 此信息将传送到结构中[**ScsiReportLuns \_ **](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_in)的**Cdb**成员的微型端口驱动程序。

*HbaPortWWN*   
用于访问目标的 HBA 的全球名称。 此信息将传送到结构[** \_ 中 ScsiReportLuns**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_in)的**HbaPortWWN**成员中的微型端口驱动程序。

*DiscoveredPortWWN*   
用于访问目标设备的端口的全球名称。 此信息将传送到结构[** \_ 中 ScsiReportLuns**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_in)的**DiscoveredPortWWN**成员中的微型端口驱动程序。

*ResponseBufferSize*   
将保存 SCSI 报表 Lun 命令结果的缓冲区的大小（以字节为单位）。 微型端口驱动程序在[**ScsiReportLuns \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)结构的**ResponseBufferSize**成员中返回此信息。

*SenseBufferSize*   
缓冲区的大小（以字节为单位），该缓冲区将保留 SCSI 报表 Lun 命令生成的 SCSI 感知数据。 微型端口驱动程序在[**ScsiReportLuns \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)结构的**SenseBufferSize**成员中返回此信息。

*ScsiStatus*   
SCSI 报表 Lun 命令的状态。 微型端口驱动程序在[**ScsiReportLuns \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)结构的**ScsiStatus**成员中返回此信息。

*ResponseBuffer*   
SCSI 报表 Lun 命令的结果。 微型端口驱动程序在[**ScsiReportLuns \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)结构的**ResponseBuffer**成员中返回此信息。

*SenseBuffer*   
Scsi 报告 Lun 命令生成的 SCSI 感知数据。 微型端口驱动程序在[**ScsiReportLuns \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)结构的**SenseBuffer**成员中返回此信息。

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


[HBA \_ 状态](hba-status.md)

[**ScsiReportLuns \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_in)

[**ScsiReportLuns \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsireportluns_out)

 

