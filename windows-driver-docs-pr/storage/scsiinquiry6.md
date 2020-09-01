---
title: ScsiInquiry 函数
description: ScsiInquiry WMI 方法向指定的设备发送 SCSI 查询命令。
ms.assetid: 31bde910-5a2a-4836-9096-d243c792e295
keywords:
- ScsiInquiry 函数存储设备
topic_type:
- apiref
api_name:
- ScsiInquiry
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 039ff9748c37394caaa7db3247a7a6155f8f7dad
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188919"
---
# <a name="scsiinquiry-function"></a>ScsiInquiry 函数


**ScsiInquiry** WMI 方法向指定的设备发送 SCSI 查询命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void ScsiInquiry(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [in] uint8                                   Cdb[6],
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[8],
   [in] uint64                                  FcLun,
   [out] uint32                                 ResponseBufferSize,
   [out] uint32                                 SenseBufferSize,
   [out] uint8                                  ScsiStatus,
   [out, WmiSizeIs("ResponseBufferSize")] uint8 ResponseBuffer[],
   [out, WmiSizeIs("SenseBufferSize")] uint8    SenseBuffer[]
);
```

<a name="parameters"></a>parameters
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out)结构的**HBAStatus**成员中返回此信息。

*Cdb*   
命令描述符块，其中包含要发送到目标设备的 SCSI 查询命令。 此信息将传送到结构中[**ScsiInquiry \_ **](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in)的**Cdb**成员的微型端口驱动程序。

*HbaPortWWN*   
用于访问目标的 HBA 的全球名称。 此信息将传送到结构[** \_ 中 ScsiInquiry**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in)的**HbaPortWWN**成员中的微型端口驱动程序。

*DiscoveredPortWWN*   
用于访问目标设备的端口的全球名称。 此信息将传送到结构[** \_ 中 ScsiInquiry**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in)的**DiscoveredPortWWN**成员中的微型端口驱动程序。

*FcLun*   
将接收 SCSI 查询命令的逻辑单元的逻辑单元号。 此信息将传送到结构[** \_ 中 ScsiInquiry**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in)的**FcLun**成员中的微型端口驱动程序。

*ResponseBufferSize*   
将保存 SCSI 查询命令结果的缓冲区的大小（以字节为单位）。 微型端口驱动程序在[**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out)结构的**ResponseBufferSize**成员中返回此信息。

*SenseBufferSize*   
缓冲区的大小（以字节为单位），该缓冲区将保存 SCSI 查询命令生成的 SCSI 感知数据。 微型端口驱动程序在[**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out)结构的**SenseBufferSize**成员中返回此信息。

*ScsiStatus*   
SCSI 查询命令的状态。 微型端口驱动程序在[**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out)结构的**ScsiStatus**成员中返回此信息。

*ResponseBuffer*   
SCSI 查询命令的结果。 微型端口驱动程序在[**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out)结构的**ResponseBuffer**成员中返回此信息。

*SenseBuffer*   
Scsi 查询命令生成的 SCSI 感知数据。 微型端口驱动程序在[**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out)结构的**SenseBuffer**成员中返回此信息。

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

[**ScsiInquiry \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_in)

[**ScsiInquiry \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_scsiinquiry_out)

 

