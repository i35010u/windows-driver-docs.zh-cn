---
title: SendCTPassThru 函数
description: SendCTPassThru WMI 方法将一个通用传输 (CT) passthrough 命令发送到指定的端口。
ms.assetid: 7f512980-5aff-4359-b52e-7fcef9627e1f
keywords:
- SendCTPassThru 函数存储设备
topic_type:
- apiref
api_name:
- SendCTPassThru
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 475e3339fe73b9a0ff4fe5d2897c39dbbd0868b5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186887"
---
# <a name="sendctpassthru-function"></a>SendCTPassThru 函数


**SendCTPassThru** WMI 方法将一个通用传输 (CT) passthrough 命令发送到指定的端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendCTPassThru(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS             HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                      PortWWN[8],
   [in] uint32                                         RequestBufferCount,
   [in, WmiSizeIs("RequestBufferCount")] uint8         RequestBuffer[],
   [out] uint32                                        TotalResponseBufferCount,
   [out] uint32                                        ActualResponseBufferCount,
   [out, WmiSizeIs("ActualResponseBufferCount")] uint8 ResponseBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**SendCTPassThru \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)结构的**HBAStatus**成员中返回此信息。

*PortWWN*   
用于访问目标的 HBA 的全球名称。 此信息将传送到结构[** \_ 中 SendCTPassThru**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_in)的**PortWWN**成员中的微型端口驱动程序。

*RequestBufferCount*   
将保存通用传输命令结果的缓冲区的大小（以字节为单位）。 微型端口驱动程序将此信息返回到结构[** \_ 中 SendCTPassThru**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_in)的**RequestBufferCount**成员。

*RequestBuffer*   
常见传输命令的结果。 微型端口驱动程序将此信息返回到结构[** \_ 中 SendCTPassThru**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_in)的**RequestBuffer**成员。

*TotalResponseBufferCount*   
结果通用传输命令的大小（以字节为单位）。 微型端口驱动程序在[**SendCTPassThru \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)结构的**TotalResponseBufferCount**成员中返回此信息。

*ActualResponseBufferCount*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在[**SendCTPassThru \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)结构的**ActualResponseBufferCount**成员中返回此信息。

*ResponseBuffer*   
常见传输命令的结果。 微型端口驱动程序在[**SendCTPassThru \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)结构的**ResponseBuffer**成员中返回此信息。

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

[**SendCTPassThru \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_in)

[**SendCTPassThru \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)

 

