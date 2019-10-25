---
title: SM\_SendCTPassThru 函数
description: SM\_SendCTPassThru WMI 方法将通用传输（CT）传递命令发送到指定的端口。
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
ms.openlocfilehash: 2d33f65e26d17829f2e018bc8fbcecbe757898e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845464"
---
# <a name="sm_sendctpassthru-function"></a>SM\_SendCTPassThru 函数


SM\_SendCTPassThru WMI 方法将通用传输（CT）传递命令发送到指定的端口。

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

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
用于访问目标的 HBA 的全球名称（WWN）。 此信息将传送到结构中 SendCTPassThru\_的 PortWWN 成员中的微型端口驱动程序。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*RequestBufferSize*   
将保存通用传输命令结果的缓冲区的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendCTPassThru 的 RequestBufferSize 成员中以结构的\_返回此信息。

*RequestBuffer*   
常见传输命令的结果。 微型端口驱动程序在 SM\_SendCTPassThru 的 RequestBuffer 成员中以结构的\_返回此信息。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SM\_SendCTPassThru\_OUT 结构的 HBAStatus 成员中返回此信息。

*TotalResponseBufferSize*   
常见传输命令的结果大小（以字节为单位）。 微型端口驱动程序在 SM\_SendCTPassThru\_OUT 结构的 TotalResponseBufferSize 成员中返回此信息。

*ActualResponseBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendCTPassThru\_OUT 结构的 ActualResponseBufferSize 成员中返回此信息。

*ResponseBuffer*   
常见传输命令的结果。 微型端口驱动程序在 SM\_SendCTPassThru\_OUT 结构的 ResponseBuffer 成员中返回此信息。

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA\_状态](hba-status.md)

[**SM\_SendCTPassThru\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendctpassthru_in)

[**SM\_SendCTPassThru\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendctpassthru_out)

 

 






