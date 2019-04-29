---
title: ScsiReadCapacity 函数
description: ScsiReadCapacity WMI 方法发送 SCSI 读取到指定设备的容量命令。
ms.assetid: 2e865ed8-a835-40e7-8ba3-babb9d18eb23
keywords:
- ScsiReadCapacity 函数存储设备
topic_type:
- apiref
api_name:
- ScsiReadCapacity
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8a9b318a7589cc5a42b132244ab4e408807d60f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378157"
---
# <a name="scsireadcapacity-function"></a>ScsiReadCapacity 函数


**ScsiReadCapacity** WMI 方法发送 SCSI 读取到指定设备的容量命令。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void ScsiReadCapacity(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS      HBAStatus,
   [in] uint8                                   Cdb[10],
   [in, HBAType("HBA_WWN")] uint8               HbaPortWWN[10],
   [in, HBAType("HBA_WWN")] uint8               DiscoveredPortWWN[10],
   [in] uint64                                  FcLun,
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
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **ScsiReadCapacity\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564910)结构。

*Cdb*   
保存 SCSI 命令描述符块读取容量命令发送到目标设备。 此信息传递到中的微型端口驱动程序**Cdb**的成员[ **ScsiReadCapacity\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564901)结构。

*HbaPortWWN*   
通过它访问目标 HBA 全球通用名称。 此信息传递到中的微型端口驱动程序**HbaPortWWN**的成员[ **ScsiReadCapacity\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564901)结构。

*DiscoveredPortWWN*   
通过它访问目标设备的端口全球通用名称。 此信息传递到中的微型端口驱动程序**DiscoveredPortWWN**的成员[ **ScsiReadCapacity\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564901)结构。

*FcLun*   
将收到 SCSI 逻辑单元的逻辑单元号读取容量命令。 此信息传递到中的微型端口驱动程序**FcLun**的成员[ **ScsiReadCapacity\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff564901)结构。

*ResponseBufferSize*   
以字节为单位的缓冲区将保留读取的容量命令的结果大小。 微型端口驱动程序将返回此信息**ResponseBufferSize**的成员[ **ScsiReadCapacity\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564910)结构。

*SenseBufferSize*   
以字节为单位的缓冲区将保留 SCSI 检测数据的 SCSI 查询命令而得出的大小。 微型端口驱动程序将返回此信息**SenseBufferSize**的成员[ **ScsiReadCapacity\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564910)结构。

*ScsiStatus*   
SCSI 状态读取容量命令。 微型端口驱动程序将返回此信息**ScsiStatus**的成员[ **ScsiReadCapacity\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564910)结构。

*ResponseBuffer*   
读取 SCSI 的结果，容量命令。 微型端口驱动程序将返回此信息**ResponseBuffer**的成员[ **ScsiReadCapacity\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564910)结构。

*SenseBuffer*   
SCSI 检测数据得出 SCSI 的读取容量命令。 微型端口驱动程序将返回此信息**SenseBuffer**的成员[ **ScsiReadCapacity\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff564910)结构。

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

[**ScsiReadCapacity\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff564901)

[**ScsiReadCapacity\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff564910)

 

 






