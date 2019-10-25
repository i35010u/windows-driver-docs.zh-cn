---
title: GetFC4Statistics 函数
description: GetFC4Statistics WMI 方法报告所指示的 FC-SW\_端口的类型为 Nx 的端口上的流量统计信息。
ms.assetid: f57f11bf-57b8-4ae9-96b3-4191f412c80c
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
ms.openlocfilehash: 18f8af9884f1d3735d3638647d69da594220105e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837966"
---
# <a name="getfc4statistics-function"></a>GetFC4Statistics 函数


**GetFC4Statistics** WMI 方法报告所指示的 Fc-sw\_端口的类型为 Nx 的端口上的流量统计信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void GetFC4Statistics(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
   [in, HBAType("HBA_WWN")] uint8          PortWWN,
   [in] uint8                              FC4Type,
   [out] MSFC_FC4STATISTICS                FC4Statistics
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，将包含一个 WMI 限定符值，该值指示操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在[**GetFC4Statistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)结构的**HBAStatus**成员中返回此信息。

*PortWWN*   
Nx 类型的本地端口的全球名称\_要报告其流量统计信息的端口。 此信息将传送到结构中[**GetFC4Statistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)的**PortWWN**成员中的微型端口驱动程序。

*FC4Type*   
一个值，该值指示类型 FC-4 协议。 有关 FC4 类型的说明，请参阅 T11 委员会*光纤通道通用服务-4*规范。 此信息将传送到结构中[**GetFC4Statistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)的**FC4Type**成员中的微型端口驱动程序。

*FC4Statistics*   
返回时，包含一个类型为[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)的结构，该结构包含指定的 FC-4 协议的统计信息。 微型端口驱动程序在[**GetFC4Statistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)结构的**FC4Statistics**成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于[MSFC\_HBAADAPTERMETHODS WMI 类](msfc-hbaadaptermethods-wmi-class.md)。

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
<td align="left">Hbapiwmi （包括 Hbapiwmi、Hbaapi 或 Hbaapi）。</td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">Hbaapi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**GetFC4Statistics\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_in)

[**GetFC4Statistics\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_getfc4statistics_out)

[HBA\_状态](hba-status.md)

[**MSFC\_FC4STATISTICS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fc4statistics)

 

 






