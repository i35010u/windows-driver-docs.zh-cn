---
title: SM\_SendRNID 函数
description: SM\_SendRNID WMI 方法向指定的端口发送请求节点标识数据（RNID）命令。
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
ms.openlocfilehash: e29155b70dce368e9306dc33cf8c69773d1723d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845457"
---
# <a name="sm_sendrnid-function"></a>SM\_SendRNID 函数


SM\_SendRNID WMI 方法向指定的端口发送请求节点标识数据（RNID）命令。

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

<a name="parameters"></a>参数
----------

*PortWWN*   
用于发送 RNID 命令的本地端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendRNID 的 PortWWN 成员中的微型端口驱动程序。

*DestWWN*   
目标端口的全球名称（WWN）。 此信息将传送到 SM\_\_SendRNID 的 DestWWN 成员中的微型端口驱动程序。

*DestFCID*   
目标端口的地址标识符。 此信息将传送到 SM\_\_SendRNID 的 DestFCID 成员中的微型端口驱动程序。

*NodeIdDataFormat*   
节点标识数据格式。 有关此成员可以具有的值的说明，请参阅 T11 委员会*光纤通道 HBA API*规范。 此信息将传送到 SM\_\_SendRNID 的 NodeIdDataFormat 成员中的微型端口驱动程序。

*InRespBufferMaxSize*   
响应缓冲区的最大大小。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序在 SM\_SendRNID\_OUT 结构的 HBAStatus 成员中返回此信息。

*TotalRespBufferSize*   
RNID 命令的结果的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendRNID\_OUT 结构的 TotalRspBufferSize 成员中返回此信息。

*ResponseBufferSize*   
RNID 命令的结果的大小（以字节为单位）。 微型端口驱动程序在 SM\_SendRNID\_OUT 结构的 ResponseBufferSize 成员中返回此信息。

*ResponseBuffer*   
RNID 命令的结果。 微型端口驱动程序在 SM\_SendRNID\_OUT 结构的 ResponseBuffer 成员中返回此信息。

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

[**SM\_SendRNID\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrnid_in)

[**SM\_SendRNID\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrnid_out)

 

 






