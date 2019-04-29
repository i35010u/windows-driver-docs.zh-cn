---
title: SM\_SendCTPassThru 函数
description: SM\_SendCTPassThru WMI 方法将常见的传输 (CT) 传递命令发送到指定的端口。
ms.assetid: 437f0c79-78f6-406e-8774-79de4425bfe8
keywords:
- SM_SendCTPassThru 函数存储设备
topic_type:
- apiref
api_name:
- SM_SendCTPassThru
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 25b0276fee830c90e681222fa078712aea7fdbfe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378939"
---
# <a name="smsendctpassthru-function"></a>SM\_SendCTPassThru 函数


SM\_SendCTPassThru WMI 方法将常见的传输 (CT) 传递命令发送到指定的端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendCTPassThru(
   [in, HBAType("HBA_WWN")] uint8              HbaPortWWN[8],
   [in] uint32                                 InRespBufferMaxSize,
   [in] uint32                                 RequestBufferSize,
   [in, WmiSizeIs("RequestBufferSize")] uint8  RequestBuffer,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalResponseBufferSize,
   [out] uint32                                ActualResponseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 ResponseBuffer[]
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN*   
通过它访问目标 HBA 全球通用名称 (WWN)。 此信息传递到 SendCTPassThru 端口全球通用名称成员中的微型端口驱动程序\_结构中。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*RequestBufferSize*   
以字节为单位，将保存常见传输命令的结果的缓冲区的大小。 微型端口驱动程序返回此信息在 SM RequestBufferSize 成员\_SendCTPassThru\_结构中。

*RequestBuffer*   
常见的传输命令的结果。 微型端口驱动程序返回此信息在 SM RequestBuffer 成员\_SendCTPassThru\_结构中。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_SendCTPassThru\_结构。

*TotalResponseBufferSize*   
以字节为单位，结果常见传输命令的大小。 微型端口驱动程序返回此信息在 SM TotalResponseBufferSize 成员\_SendCTPassThru\_结构。

*ActualResponseBufferSize*   
以字节为单位的实际检索数据的大小。 微型端口驱动程序返回此信息在 SM ActualResponseBufferSize 成员\_SendCTPassThru\_结构。

*ResponseBuffer*   
常见的传输命令的结果。 微型端口驱动程序返回此信息在 SM ResponseBuffer 成员\_SendCTPassThru\_结构。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS\_SM\_FabricAndDomainManagementMethods WMI 类。

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

[**SM\_SendCTPassThru\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566293)

[**SM\_SendCTPassThru\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff566294)

 

 






