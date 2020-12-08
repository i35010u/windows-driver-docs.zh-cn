---
title: SM \_ SendCTPassThru 函数
description: SM \_ SENDCTPASSTHRU WMI 方法将通用传输 (CT) 传递命令发送到指定的端口。
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
ms.openlocfilehash: cea559dfee53af20cb8e4db90aa853f057da3adc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792571"
---
# <a name="sm_sendctpassthru-function"></a>SM \_ SendCTPassThru 函数


SM \_ SENDCTPASSTHRU WMI 方法将通用传输 (CT) 传递命令发送到指定的端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendCTPassThru(
   [in, HBAType("HBA_WWN")] uint8              HbaPortWWN[8],
   [in] uint32                                 InRespBufferMaxSize,
   [in] uint32                                 RequestBufferSize,
   [in, WmiSizeIs("RequestBufferSize")] uint8  RequestBuffer,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalResponseBufferSize,
   [out] uint32                                ActualResponseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 ResponseBuffer[]
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
用于访问目标的 HBA 的全球名称 (WWN) 。 此信息将传送到结构中 SendCTPassThru 的 PortWWN 成员中的微型端口驱动程序 \_ 。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*RequestBufferSize*   
将保存通用传输命令结果的缓冲区的大小（以字节为单位）。 微型端口驱动程序将此信息返回到 SM \_ SendCTPassThru 结构中的 RequestBufferSize 成员 \_ 。

*RequestBuffer*   
常见传输命令的结果。 微型端口驱动程序将此信息返回到 SM \_ SendCTPassThru 结构中的 RequestBuffer 成员 \_ 。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 SM \_ SendCTPassThru OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

*TotalResponseBufferSize*   
常见传输命令的结果大小（以字节为单位）。 微型端口驱动程序在 SM \_ SendCTPassThru OUT 结构的 TotalResponseBufferSize 成员中返回此信息 \_ 。

*ActualResponseBufferSize*   
实际检索到的数据的大小（以字节为单位）。 微型端口驱动程序在 SM \_ SendCTPassThru OUT 结构的 ActualResponseBufferSize 成员中返回此信息 \_ 。

*ResponseBuffer*   
常见传输命令的结果。 微型端口驱动程序在 SM \_ SendCTPassThru OUT 结构的 ResponseBuffer 成员中返回此信息 \_ 。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS \_ SM \_ FabricAndDomainManagementMethods WMI 类。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SM \_ SendCTPassThru \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendctpassthru_in)

[**SM \_ SendCTPassThru \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendctpassthru_out)

 

