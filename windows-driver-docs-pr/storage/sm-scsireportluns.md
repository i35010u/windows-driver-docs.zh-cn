---
title: SM\_ScsiReportLuns 函数
description: SM\_ScsiReportLuns WMI 方法将 SCSI 报表 Lun 命令发送到指定的设备。
ms.assetid: 846efe8a-dc36-4601-882d-aeb9c53d09dc
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
ms.openlocfilehash: 7676a1c4c77004d25e8ca0c0cc0f0c56ed2812dd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522008"
---
# <a name="smscsireportluns-function"></a>SM\_ScsiReportLuns 函数


SM\_ScsiReportLuns WMI 方法将 SCSI 报表 Lun 命令发送到指定的设备。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_ScsiReportLuns(
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8               DomainPortWWN[8],
   [in, HBAType("HBA_SCSILUN")] uint64          SmhbaLUN,
   [in] uint8                                   Cdb[12],
   [in] uint32                                  InRespBufferMaxSize,
   [in] uint32                                  InSenseBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [out] uint8                                  ScsiStatus,
   [out] uint32                                 TotalRespBufferSize,
   [out] uint32                                 OutRespBufferSize,
   [out] uint32                                 OutSenseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8  RespBuffer[],
   [out, WmiSizeIs("OutSenseBufferSize")] uint8 SenseBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
通过它访问目标 HBA 全球通用名称 (WWN)。 此信息传递到的 HbaPortWWN 成员中的微型端口驱动程序[ **ScsiInquiry\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564598)结构。

*DiscoveredPortWWN*   
通过它访问目标设备的端口全球通用名称 (WWN)。 此信息传递到的 DiscoveredPortWWN 成员中的微型端口驱动程序[ **ScsiInquiry\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564598)结构。

*DomainPortWWN*   
全球通用名称 (WWN) 的回调。 是的端口\_具有任何端口的最小值的标识符\_发现使用的物理端口的 SMP 端口的标识符。 如果没有 SMP 端口已发现使用的物理端口，它具有值为零。

*SmhbaLUN*   
将收到的 SCSI 查询命令的逻辑单元将逻辑单元号。 此信息传递到的 SmhbaLUN 成员中的微型端口驱动程序[ **ScsiInquiry\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564598)结构。

*Cdb*   
包含要发送到目标设备的 SCSI 查询命令命令描述符块。 此信息传递到的 Cdb 成员中的微型端口驱动程序[ **ScsiInquiry\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564598)结构。

*InRespBufferMaxSize*   
以字节为单位，响应缓冲区的最大大小。

*InSenseBufferMaxSize*   
最大大小，以字节为单位，在响应中有意义缓冲区。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息中 HBAStatus 隶属[ **ScsiInquiry\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564604)结构。

*ScsiStatus*   
SCSI 查询命令的状态。 微型端口驱动程序返回此信息中 ScsiStatus 隶属[ **ScsiInquiry\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564604)结构。

*TotalRespBufferSize*   
以字节为单位的报表 lun 命令的结果的大小。

*OutRespBufferSize*   
以字节为单位，将保存的 SCSI 查询命令结果的缓冲区的大小。 微型端口驱动程序返回此信息中 ResponseBufferSize 隶属[ **ScsiInquiry\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564604)结构。

*OutSenseBufferSize*   
以字节为单位，将保存的 SCSI 查询命令结果 SCSI 意义上数据的缓冲区的大小。 微型端口驱动程序返回此信息中 SenseBufferSize 隶属[ **ScsiInquiry\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564604)结构。

*RespBuffer*   
SCSI 查询命令的结果。 微型端口驱动程序返回此信息中 ResponseBuffer 隶属[ **ScsiInquiry\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564604)结构。

*SenseBuffer*   
SCSI 检测数据得出的 SCSI 查询命令。 微型端口驱动程序返回此信息中 SenseBuffer 隶属[ **ScsiInquiry\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564604)结构。

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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

 

 






