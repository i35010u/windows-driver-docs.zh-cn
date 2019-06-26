---
title: SendRNIDV2 函数
description: SendRNIDV2 WMI 方法将版本 2 RNID 命令发送到指定的端口。
ms.assetid: ac9304b3-498b-4349-befd-529a4978bb52
keywords:
- SendRNIDV2 函数存储设备
topic_type:
- apiref
api_name:
- SendRNIDV2
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f1e8d47913b215bba7052bf45d7b7411095934f4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362660"
---
# <a name="sendrnidv2-function"></a>SendRNIDV2 函数


**SendRNIDV2** WMI 方法将第 2 版 RNID 命令发送到指定的端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendRNIDV2(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [in] uint32                                   DestFCID,
   [in] uint32                                   NodeIdDataFormat,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **SendRNIDV2\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)结构。

*PortWWN*   
通过其发送的版本 2 RNID 命令的本地端口全球通用名称。 此信息传递到中的微型端口驱动程序**端口全球通用名称**的成员[ **SendRNIDV2\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)结构。

*DestWWN*   
目标端口全球通用名称。 此信息传递到中的微型端口驱动程序**DestWWN**的成员[ **SendRNIDV2\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)结构。

*DestFCID*   
目标端口地址标识符。 此信息传递到中的微型端口驱动程序**DestFCID**的成员[ **SendRNIDV2\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)结构。

*NodeIdDataFormat*   
节点标识数据格式。 可以为此成员的值的说明，请参阅 T11 委员会*光纤通道 HBA API*规范。 此信息传递到中的微型端口驱动程序**NodeIdDataFormat**的成员[ **SendRNIDV2\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)结构。

*TotalRspBufferSize*   
以字节为单位的版本 2 RNID 命令的结果大小。 微型端口驱动程序将返回此信息**TotalRspBufferSize**的成员[ **SendRNIDV2\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)结构。

*ActualRspBufferSize*   
以字节为单位的实际检索的数据大小。 微型端口驱动程序将返回此信息**ActualRspBufferSize**的成员[ **SendRNIDV2\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)结构。

*RspBuffer*   
版本 2 RNID 命令的结果。 微型端口驱动程序将返回此信息**RspBuffer**的成员[ **SendRNIDV2\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)结构。

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

[**SendRNIDV2\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)

[**SendRNIDV2\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)

 

 






