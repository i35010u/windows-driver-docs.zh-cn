---
title: SendSRL 函数
description: SendSRL WMI 方法将通过指示端口扫描远程循环 (SRL) 命令发送到指定的域控制器。
ms.assetid: b191fc8c-2765-4e39-aab7-e950ae1d46b0
keywords:
- SendSRL 函数存储设备
topic_type:
- apiref
api_name:
- SendSRL
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 99979f70e58d3b5531f95d3cb65aa88070b9b02d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362647"
---
# <a name="sendsrl-function"></a>SendSRL 函数


**SendSRL** WMI 方法将通过指示端口扫描远程循环 (SRL) 命令发送到指定的域控制器。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendSRL(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                WWN[8],
   [in] uint32                                   Domain,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>Parameters
----------

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **SendSRL\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendsrl_out)结构。

*PortWWN*   
通过其发送的 SRL 命令的本地端口全球通用名称。 此信息传递到中的微型端口驱动程序**端口全球通用名称**SendSRL 成员\_结构中。

*WWN*   
类型佛罗里达州的端口的全球名称\_其循环是要扫描的端口。 此信息传递到中的微型端口驱动程序**WWN** SendSRL 成员\_结构中。

*域*   
其循环是要扫描的域域数。 此信息传递到中的微型端口驱动程序**域**SendSRL 成员\_结构中。

*TotalRspBufferSize*   
以字节为单位的 SRL 命令的结果大小。 微型端口驱动程序将返回此信息**TotalRspBufferSize**的成员[ **SendSRL\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendsrl_out)结构。

*ActualRspBufferSize*   
以字节为单位的实际检索的数据大小。 微型端口驱动程序将返回此信息**ActualRspBufferSize**的成员[ **SendSRL\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendsrl_out)结构。

*RspBuffer*   
SRL 命令的结果。 微型端口驱动程序将返回此信息**RspBuffer**的成员[ **SendSRL\_OUT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendsrl_out)结构。

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

SendSRL\_IN [**SendSRL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendsrl_out)

 

 






