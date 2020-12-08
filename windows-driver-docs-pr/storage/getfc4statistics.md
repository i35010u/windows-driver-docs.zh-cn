---
title: GetFC4Statistics 函数
description: GetFC4Statistics WMI 方法 \_ 针对指定的 fc-sw 协议报告 Nx 端口类型端口上的流量统计信息。
keywords:
- GetFC4Statistics 函数存储设备
topic_type:
- apiref
api_name:
- GetFC4Statistics
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49ba736187ac2bedd04da0e246ed29fcd95134da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835255"
---
# <a name="getfc4statistics-function"></a>GetFC4Statistics 函数


**GetFC4Statistics** WMI 方法 \_ 针对指定的 Fc-sw 协议报告 Nx 端口类型端口上的流量统计信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFC4Statistics(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in, HBAType("HBA_WWN")] uint8          PortWWN,
   [in] uint8                              FC4Type,
   [out] MSFC_FC4STATISTICS                FC4Statistics
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，将包含一个 WMI 限定符值，该值指示操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**GetFC4Statistics \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)结构的 **HBAStatus** 成员中返回此信息。

*PortWWN*   
\_要报告其流量统计信息的 Nx 端口类型的本地端口的全球名称。 此信息将传送到结构 [**\_ 中 GetFC4Statistics**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)的 **PortWWN** 成员中的微型端口驱动程序。

*FC4Type*   
一个值，该值指示类型 FC-4 协议。 有关 FC4 类型的说明，请参阅 T11 委员会 *光纤通道通用服务-4* 规范。 此信息将传送到结构 [**\_ 中 GetFC4Statistics**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)的 **FC4Type** 成员中的微型端口驱动程序。

*FC4Statistics*   
返回时，包含 [**MSFC \_ FC4STATISTICS**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics) 类型的结构，该结构包含指定的 fc-sw 协议的统计信息。 微型端口驱动程序在 [**GetFC4Statistics \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)结构的 **FC4Statistics** 成员中返回此信息。

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
<td align="left">台式机</td>
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


[**GetFC4Statistics \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)

[**GetFC4Statistics \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)

[HBA \_ 状态](hba-status.md)

[**MSFC \_ FC4STATISTICS**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

 

