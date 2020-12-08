---
title: IPrinterScriptUsbJobContext ReturnCodes 方法
description: 返回一个对象，该对象可提供 IHV 为其 JavaScript 函数定义的返回代码值。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- ReturnCodes 方法打印设备
- ReturnCodes 方法打印设备，IPrinterScriptUsbJobContext 接口
- IPrinterScriptUsbJobContext 接口打印设备，ReturnCodes 方法
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.ReturnCodes
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 423575cc9f890262f8f5799bd90efec729a26480
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796605"
---
# <a name="iprinterscriptusbjobcontextreturncodes-method"></a>IPrinterScriptUsbJobContext：： ReturnCodes 方法

返回一个对象，该对象可提供 IHV 为其 JavaScript 函数定义的返回代码值。

<a name="syntax"></a>语法
------

```cpp
HRESULT ReturnCodes(
  [out, retval] IPrinterScriptUsbJobContextReturnCodes **ppReturnCodes
);
```

<a name="parameters"></a>参数
----------

*ppReturnCodes* \[out，retval\]  
IHV JavaScript 函数的返回代码值。 返回代码值由 [**IPrinterScriptUsbJobContextReturnCodes**](iprinterscriptusbjobcontextreturncodes.md) 接口表示。

<a name="return-value"></a>返回值
------------

此方法返回 **HRESULT** 值。

<a name="remarks"></a>备注
-------

IHV 必须开发一个接口，该接口可实现与当前打印作业关联的属性包。 然后，IHV JavaScript 函数可以使用此属性包存储特定于当前正在处理的打印作业的属性或数据。 此属性包在当前作业的持续时间内存在。

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

[**IPrinterScriptUsbJobContextReturnCodes**](iprinterscriptusbjobcontextreturncodes.md)
