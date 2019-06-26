---
title: SM\_SendRNID 函数
description: SM\_SendRNID WMI 方法将请求节点标识数据 (RNID) 命令发送到指定的端口。
ms.assetid: 160e2dc7-8195-4f8a-bc59-854e5283cf6f
keywords:
- SM_SendRNID 函数存储设备
topic_type:
- apiref
api_name:
- SM_SendRNID
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 82914753dfbcaee06b7ba11414e6252af0af9083
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384284"
---
# <a name="smsendrnid-function"></a>SM\_SendRNID 函数


SM\_SendRNID WMI 方法将请求节点标识数据 (RNID) 命令发送到指定的端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_SendRNID(
   [in, HBAType("HBA_WWN")] uint8              PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              DestWWN[8],
   [in] uint32                                 DestFCID,
   [in] uint32                                 NodeIdDataFormat,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                ResponseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 ResponseBuffer[]
);
```

<a name="parameters"></a>Parameters
----------

*PortWWN*   
通过其发送 RNID 命令的本地端口全球通用名称 (WWN)。 此信息传递到 SM 端口全球通用名称成员中的微型端口驱动程序\_SendRNID\_结构中。

*DestWWN*   
目标端口全球通用名称 (WWN)。 此信息传递到 SM DestWWN 成员中的微型端口驱动程序\_SendRNID\_结构中。

*DestFCID*   
目标端口地址标识符。 此信息传递到 SM DestFCID 成员中的微型端口驱动程序\_SendRNID\_结构中。

*NodeIdDataFormat*   
节点标识数据格式。 可以为此成员的值的说明，请参阅 T11 委员会*光纤通道 HBA API*规范。 此信息传递到 SM NodeIdDataFormat 成员中的微型端口驱动程序\_SendRNID\_结构中。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序返回此信息在 SM HBAStatus 成员\_SendRNID\_结构。

*TotalRespBufferSize*   
以字节为单位，RNID 命令的结果的大小。 微型端口驱动程序返回此信息在 SM TotalRspBufferSize 成员\_SendRNID\_结构。

*ResponseBufferSize*   
以字节为单位，RNID 命令的结果的大小。 微型端口驱动程序返回此信息在 SM ResponseBufferSize 成员\_SendRNID\_结构。

*ResponseBuffer*   
RNID 命令的结果。 微型端口驱动程序返回此信息在 SM ResponseBuffer 成员\_SendRNID\_结构。

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

[**SM\_SendRNID\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_sendrnid_in)

[**SM\_SendRNID\_出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_sendrnid_out)

 

 






