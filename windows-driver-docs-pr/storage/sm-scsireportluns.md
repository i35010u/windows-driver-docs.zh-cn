---
title: SM \_ ScsiReportLuns 函数
description: SM \_ SCSIREPORTLUNS WMI 方法可向所指示的设备发送 SCSI 报表 lun 命令。
keywords:
- SM_ScsiReportLuns 函数存储设备
topic_type:
- apiref
api_name:
- SM_ScsiReportLuns
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cdab9861153ac4e69fa3e7e861fcb88461894a79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792573"
---
# <a name="sm_scsireportluns-function"></a>SM \_ ScsiReportLuns 函数


SM \_ SCSIREPORTLUNS WMI 方法可向所指示的设备发送 SCSI 报表 lun 命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_ScsiReportLuns(
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DomainPortWWN[8],
   [in, HBAType("HBA_SCSILUN")] uint64          SmhbaLUN,
   [in] uint8                                   Cdb[12],
   [in] uint32                                  InRespBufferMaxSize,
   [in] uint32                                  InSenseBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [out] uint8                                  ScsiStatus,
   [out] uint32                                 TotalRespBufferSize,
   [out] uint32                                 OutRespBufferSize,
   [out] uint32                                 OutSenseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8  RespBuffer[],
   [out, WmiSizeIs("OutSenseBufferSize")] uint8 SenseBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
用于访问目标的 HBA 的全球名称 (WWN) 。 此信息将传送到结构 [**\_ 中 ScsiInquiry**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in) 的 HbaPortWWN 成员中的微型端口驱动程序。

*DiscoveredPortWWN*   
用于访问目标设备的端口的全球名称 (WWN) 。 此信息将传送到结构 [**\_ 中 ScsiInquiry**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in) 的 DiscoveredPortWWN 成员中的微型端口驱动程序。

*DomainPortWWN*   
用于回调的全球名称 (WWN) 。 它是端口 \_ 标识符，它具有 \_ 使用物理端口发现的 SMP 端口的任何端口标识符的最小值。 如果未使用物理端口发现任何 SMP 端口，则它的值为零。

*SmhbaLUN*   
将接收 SCSI 查询命令的逻辑单元的逻辑单元号。 此信息将传送到结构 [**\_ 中 ScsiInquiry**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in) 的 SmhbaLUN 成员中的微型端口驱动程序。

*Cdb*   
命令描述符块，其中包含要发送到目标设备的 SCSI 查询命令。 此信息将传送到结构中 [**ScsiInquiry \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in) 的 Cdb 成员的微型端口驱动程序。

*InRespBufferMaxSize*   
响应缓冲区的最大大小（以字节为单位）。

*InSenseBufferMaxSize*   
响应中的感知缓冲区的最大大小（以字节为单位）。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out) 结构的 HBAStatus 成员中返回此信息。

*ScsiStatus*   
SCSI 查询命令的状态。 微型端口驱动程序在 [**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out) 结构的 ScsiStatus 成员中返回此信息。

*TotalRespBufferSize*   
报表 lun 命令的结果的大小（以字节为单位）。

*OutRespBufferSize*   
将保存 SCSI 查询命令结果的缓冲区的大小（以字节为单位）。 微型端口驱动程序在 [**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out) 结构的 ResponseBufferSize 成员中返回此信息。

*OutSenseBufferSize*   
缓冲区的大小（以字节为单位），该缓冲区将保存 SCSI 查询命令生成的 SCSI 感知数据。 微型端口驱动程序在 [**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out) 结构的 SenseBufferSize 成员中返回此信息。

*RespBuffer*   
SCSI 查询命令的结果。 微型端口驱动程序在 [**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out) 结构的 ResponseBuffer 成员中返回此信息。

*SenseBuffer*   
Scsi 查询命令生成的 SCSI 感知数据。 微型端口驱动程序在 [**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out) 结构的 SenseBuffer 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS \_ SM \_ ScsiInformationMethods WMI 类。

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
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

 

