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
ms.openlocfilehash: 5693d52c6646f94267de16d5f5cd5af65657e861
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561907"
---
# <a name="scsireportluns-function"></a>ScsiReportLuns 函数


**ScsiReportLuns** WMI 方法将 SCSI 报表 Lun 命令发送到指定的设备。

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

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **ScsiReportLuns\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564937)结构。

*Cdb*   
命令描述符块包含 SCSI 报表 Lun 命令发送到目标设备。 此信息传递到中的微型端口驱动程序**Cdb**的成员[ **ScsiReportLuns\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564932)结构。

*HbaPortWWN*   
通过它访问目标 HBA 全球通用名称。 此信息传递到中的微型端口驱动程序**HbaPortWWN**的成员[ **ScsiReportLuns\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564932)结构。

*DiscoveredPortWWN*   
通过它访问目标设备的端口全球通用名称。 此信息传递到中的微型端口驱动程序**DiscoveredPortWWN**的成员[ **ScsiReportLuns\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564932)结构。

*ResponseBufferSize*   
以字节为单位的缓冲区将保留 SCSI 报告 Lun 命令的结果的大小。 微型端口驱动程序将返回此信息**ResponseBufferSize**的成员[ **ScsiReportLuns\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564937)结构。

*SenseBufferSize*   
从 SCSI 报表 Lun 命令结果以字节为单位的缓冲区将保留 SCSI 检测数据的大小。 微型端口驱动程序将返回此信息**SenseBufferSize**的成员[ **ScsiReportLuns\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564937)结构。

*ScsiStatus*   
SCSI 报表 Lun 命令的状态。 微型端口驱动程序将返回此信息**ScsiStatus**的成员[ **ScsiReportLuns\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564937)结构。

*ResponseBuffer*   
SCSI 的结果将报告 Lun 命令。 微型端口驱动程序将返回此信息**ResponseBuffer**的成员[ **ScsiReportLuns\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564937)结构。

*SenseBuffer*   
生成从 SCSI 的 SCSI 意义上数据报告 Lun 命令。 微型端口驱动程序将返回此信息**SenseBuffer**的成员[ **ScsiReportLuns\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564937)结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_HBAAdapterMethods WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left">Hbapiwmi.h （包括 Hbapiwmi.h、 Hbaapi.h 或 Hbaapi.h）</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**ScsiReportLuns\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff564932)

[**ScsiReportLuns\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff564937)

 

 






