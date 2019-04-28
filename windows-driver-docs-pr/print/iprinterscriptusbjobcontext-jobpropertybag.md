---
title: IPrinterScriptUsbJobContext JobPropertyBag 方法
description: 返回与当前打印作业相关联的属性包。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 6309CCD2-D53A-4B21-970E-AF19D1DACEE3
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
ms.openlocfilehash: 9f31afd0131ee0b0c89d83c0608108fbeacd8e8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349251"
---
# <a name="iprinterscriptusbjobcontextjobpropertybag-method"></a>IPrinterScriptUsbJobContext::JobPropertyBag 方法

返回与当前打印作业相关联的属性包。

<a name="syntax"></a>语法
------

```cpp
HRESULT JobPropertyBag(
  [out, retval] IPrinterScriptablePropertyBag **ppPropertyBag
);
```

<a name="parameters"></a>Parameters
----------

*ppPropertyBag* \[out, retval\]  
属性包与当前打印作业相关联。

<a name="return-value"></a>返回值
------------

此方法返回**HRESULT**值。

<a name="remarks"></a>备注
-------

**JobPropertyBag**是只读的方法。 IHV JavaScript 函数可以使用此属性包来存储属性或特定于当前正在处理打印作业的数据。 当前作业的持续期间存在此属性包。

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
