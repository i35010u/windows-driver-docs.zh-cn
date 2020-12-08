---
title: IPrinterScriptUsbJobContext JobPropertyBag 方法
description: 返回与当前打印作业关联的属性包。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- JobPropertyBag 方法打印设备
- JobPropertyBag 方法打印设备，IPrinterScriptUsbJobContext 接口
- IPrinterScriptUsbJobContext 接口打印设备，JobPropertyBag 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.JobPropertyBag
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 992b5a94746c9e5ae937661d770c33f4d71d8d3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835561"
---
# <a name="iprinterscriptusbjobcontextjobpropertybag-method"></a>IPrinterScriptUsbJobContext：： JobPropertyBag 方法

返回与当前打印作业关联的属性包。

<a name="syntax"></a>语法
------

```cpp
HRESULT JobPropertyBag(
  [out, retval] IPrinterScriptablePropertyBag **ppPropertyBag
);
```

<a name="parameters"></a>参数
----------

*ppPropertyBag* \[out，retval\]  
与当前打印作业关联的属性包。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="remarks"></a>备注
-------

**JobPropertyBag** 为只读方法。 IHV JavaScript 函数可以使用此属性包来存储特定于当前正在处理的打印作业的属性或数据。 此属性包在当前作业的持续时间内存在。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p>目标平台</p></td>
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)
