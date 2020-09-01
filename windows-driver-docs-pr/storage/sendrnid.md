---
title: SendRNID 函数
description: SendRNID WMI 方法将请求节点标识数据 (RNID) 命令发送到指定的端口。
ms.assetid: 70c9655c-aaa8-45bb-ae5b-7428d9cdd4b2
keywords:
- SendRNID 函数存储设备
topic_type:
- apiref
api_name:
- SendRNID
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 78080bc8bfd8b4c9a12a5fdddf0c0ac4809eef7a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186867"
---
# <a name="sendrnid-function"></a>SendRNID 函数


**SendRNID** WMI 方法将请求节点标识数据 (RNID) 命令发送到指定的端口。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SendRNID(
   [in, HBAType("HBA_WWN")] uint8                                                          wwn[8],
   [in, HBAType("HBA_WWNTYPE"), Values{"NODE_WWN", "PORT_WWN"}, ValueMap{"0", "1"}] uint32 wwntype,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                                                 HBAStatus,
   [out] uint32                                                                            ResponseBufferCount,
   [out, WmiSizeIs("ResponseBufferCount")] uint8                                           ResponseBuffer[]
);
```

<a name="parameters"></a>参数
----------

*wwn*   
RNID 命令发送到的端口的全球名称。 此信息将传送到 SendRNID 结构中的 **wwn** 成员的微型端口 [**驱动 \_ **](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_in) 程序。

*wwntype*   
已否决。 请勿使用。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在[**SendRNID \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_out)结构的**HBAStatus**成员中返回此信息。

*ResponseBufferCount*   
RNID 命令的结果的大小（以字节为单位）。 微型端口驱动程序在[**SendRNID \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_out)结构的**ResponseBufferCount**成员中返回此信息。

*ResponseBuffer*   
RNID 命令的结果。 微型端口驱动程序在[**SendRNID \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_out)结构的**ResponseBuffer**成员中返回此信息。

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

[**SendRNID \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_in)

[**SendRNID \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_out)

 

