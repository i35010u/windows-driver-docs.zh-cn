---
title: IPrinterScriptUsbJobContext ReturnCodes 方法
description: 返回一个对象，可以提供 IHV 已定义的 JavaScript 函数的返回代码值。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 0FD3A103-970E-4EB8-9867-7EC21273269C
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
ms.openlocfilehash: 9db76f31b4e7088d889b5fc07ef0d29109a1f047
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349237"
---
# <a name="iprinterscriptusbjobcontextreturncodes-method"></a>IPrinterScriptUsbJobContext::ReturnCodes 方法

返回一个对象，可以提供 IHV 已定义的 JavaScript 函数的返回代码值。

<a name="syntax"></a>语法
------

```cpp
HRESULT ReturnCodes(
  [out, retval] IPrinterScriptUsbJobContextReturnCodes **ppReturnCodes
);
```

<a name="parameters"></a>Parameters
----------

*ppReturnCodes* \[out, retval\]  
IHV JavaScript 函数的返回代码值。 返回代码值由[ **IPrinterScriptUsbJobContextReturnCodes** ](iprinterscriptusbjobcontextreturncodes.md)接口。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

IHV 必须开发实现与当前打印作业关联的属性包的接口。 然后，IHV JavaScript 函数可以使用此属性包来存储属性或特定于当前正在处理打印作业的数据。 当前作业的持续期间存在此属性包。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)

[**IPrinterScriptUsbJobContextReturnCodes**](iprinterscriptusbjobcontextreturncodes.md)
