---
title: SM\_ScsiReadCapacity 函数
description: SM\_ScsiReadCapacity WMI 方法可向所指示的设备发送 SCSI 读取容量命令。
ms.assetid: 2b9bc0b0-1a4f-4a65-a009-1d92fa6c3fa0
keywords:
- SM_ScsiReadCapacity 函数存储设备
topic_type:
- apiref
api_name:
- SM_ScsiReadCapacity
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4fd5dbdbb5094dc33839e2144e34cef2bf0c348f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845468"
---
# <a name="sm_scsireadcapacity-function"></a>SM\_ScsiReadCapacity 函数


SM\_ScsiReadCapacity WMI 方法可向所指示的设备发送 SCSI 读取容量命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_ScsiReadCapacity(
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DomainPortWWN[8],
   [in, HBAType("HBA_SCSILUN")] uint64          SmhbaLUN,
   [in] uint8                                   Cdb[16],
   [in] uint32                                  InRespBufferMaxSize,
   [in] uint32                                  InSenseBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [out] uint8                                  ScsiStatus,
   [out] uint32                                 OutRespBufferSize,
   [out] uint32                                 OutSenseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8  RespBuffer[],
   [out, WmiSizeIs("OutSenseBufferSize")] uint8 SenseBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
用于访问目标的 HBA 的全球名称（WWN）。 此信息将传送到结构中[**ScsiInquiry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)的 HbaPortWWN 成员中的微型端口驱动程序。

*DiscoveredPortWWN*   
用于访问目标设备的端口的全球名称（WWN）。 此信息将传送到结构中[**ScsiInquiry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)的 DiscoveredPortWWN 成员中的微型端口驱动程序。

*DomainPortWWN*   
用于回调的全球名称（WWN）。 端口\_标识符，它具有使用物理端口发现的 SMP 端口\_标识符的最小值。 如果未使用物理端口发现任何 SMP 端口，则它的值为零。

*SmhbaLUN*   
将接收 SCSI 查询命令的逻辑单元的逻辑单元号。 此信息将传送到结构中[**ScsiInquiry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)的 SmhbaLUN 成员中的微型端口驱动程序。

*Cdb*   
命令描述符块，其中包含要发送到目标设备的 SCSI 查询命令。 此信息会以结构中[**ScsiInquiry\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)的 Cdb 成员的形式传递到微型端口驱动程序。

*InRespBufferMaxSize*   
响应缓冲区的最大大小（以字节为单位）。

*InSenseBufferMaxSize*   
响应中的感知缓冲区的最大大小（以字节为单位）。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)结构的 HBAStatus 成员中返回此信息。

*ScsiStatus*   
SCSI 查询命令的状态。 微型端口驱动程序在[**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)结构的 ScsiStatus 成员中返回此信息。

*OutRespBufferSize*   
将保存 SCSI 查询命令结果的缓冲区的大小（以字节为单位）。 微型端口驱动程序在[**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)结构的 ResponseBufferSize 成员中返回此信息。

*OutSenseBufferSize*   
缓冲区的大小（以字节为单位），该缓冲区将保存 SCSI 查询命令生成的 SCSI 感知数据。 微型端口驱动程序在[**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)结构的 SenseBufferSize 成员中返回此信息。

*RespBuffer*   
SCSI 查询命令的结果。 微型端口驱动程序在[**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)结构的 ResponseBuffer 成员中返回此信息。

*SenseBuffer*   
Scsi 查询命令生成的 SCSI 感知数据。 微型端口驱动程序在[**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)结构的 SenseBuffer 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_ScsiInformationMethods WMI 类。

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

 

 






