---
title: GetFcpTargetMapping 函数
description: GetFcpTargetMapping WMI 方法检索这些逻辑单元的唯一标识一系列的操作系统的逻辑单元的信息和光纤通道协议 (FCP) 标识符之间的映射。
ms.assetid: 2e4b3554-31de-4eaa-9228-844639a219d5
keywords:
- GetFcpTargetMapping 函数存储设备
topic_type:
- apiref
api_name:
- GetFcpTargetMapping
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a75f142476a2863f5b6aa7afb9cf70fd18a38696
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378537"
---
# <a name="getfcptargetmapping-function"></a>GetFcpTargetMapping 函数


**GetFcpTargetMapping** WMI 方法检索这些逻辑单元的唯一标识一系列的操作系统的逻辑单元的信息和光纤通道协议 (FCP) 标识符之间的映射。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFcpTargetMapping(
   [in, HBAType("HBA_WWN")] uint8                    HbaPortWWN[8],
   [in] uint32                                       InEntryCount,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS           HBAStatus,
   [out] uint32                                      TotalEntryCount,
   [out] uint32                                      OutEntryCount,
   [out, WmiSizeIs("OutEntryCount")] HBAFCPScsiEntry Entry[]
);
```

<a name="parameters"></a>Parameters
----------

*HbaPortWWN\[8\]*    
要检索其表映射的端口全球通用名称。 此信息传递到中的微型端口驱动程序**HbaPortWWN**的成员[ **GetFcpTargetMapping\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_in)结构。

*InEntryCount*   
指示 WMI 提供程序可以报告中的绑定项数*条目*参数。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **GetFcpTargetMapping\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_out)结构。

*TotalEntryCount*   
指示与 HBA 相关联的持久绑定的总数。

*OutEntryCount*   
指示映射检索的总数量**GetFcpTargetMapping**方法。 此值将为小于或等于*TotalEntryCount*。

*条目\[\]*    
类型的结构数组[ **HBAFCPScsiEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_hbafcpscsientry) ，描述操作系统与光纤通道协议 (FCP) 标识符之间的 HBA 的绑定。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_HBAFCPInfo WMI 类](msfc-hbafcpinfo-wmi-class.md)。

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

[**GetFcpTargetMapping\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_in)

[**GetFcpTargetMapping\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_getfcptargetmapping_out)

 

 






