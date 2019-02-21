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
ms.openlocfilehash: 3b2173c904da6ec23cf0b27cb32ee0a609f5ef4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525942"
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
RNID 命令发送到的端口全球通用名称。 此信息传递到中的微型端口驱动程序**wwn**的成员[ **SendRNID\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565485)结构。

*wwntype*   
已弃用。 不使用。

*HBAStatus*   
在返回时包含操作的状态。 允许的值及其说明的列表，请参阅[HBA\_状态](hba-status.md)。 微型端口驱动程序将返回此信息**HBAStatus**的成员[ **SendRNID\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565486)结构。

*ResponseBufferCount*   
以字节为单位的 RNID 命令的结果大小。 微型端口驱动程序将返回此信息**ResponseBufferCount**的成员[ **SendRNID\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565486)结构。

*ResponseBuffer*   
RNID 命令的结果。 微型端口驱动程序将返回此信息**ResponseBuffer**的成员[ **SendRNID\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/ff565486)结构。

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
<td align="left"><p>标头</p></td>
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

[**SendRNID\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565485)

[**SendRNID\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff565486)

 

 






