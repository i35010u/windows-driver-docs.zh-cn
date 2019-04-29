---
title: Iasphelp get\_MibErrorDscp 方法
description: MibErrorDscp 属性启用 ASP Web 页后，可以将一个简单网络管理协议 (SNMP) 管理信息基础 (MIB) 的错误代码转换成错误的文本说明。
MS-HAID:
- webfnc\_3931fbc6-1960-4d40-a6e3-8816ee832c89.xml
- print.iasphelp\_miberrordscp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: b2ab9414-8401-4ec4-a235-f6a8da93523b
keywords:
- get_MibErrorDscp 方法打印设备
- get_MibErrorDscp 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_MibErrorDscp 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_MibErrorDscp
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba6acc8a6a5d9e39e823dcee7d687e7ac56bbc5b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392831"
---
# <a name="iasphelpgetmiberrordscp-method"></a>Iasphelp::get\_MibErrorDscp 方法

**MibErrorDscp**属性启用 ASP Web 页后，可以将一个简单网络管理协议 (SNMP) 管理信息基础 (MIB) 的错误代码转换成错误的文本说明。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_MibErrorDscp(
  [in]  DWORD dwError,
  [out] BSTR  *pVal
);
```

<a name="parameters"></a>Parameters
----------

*dwError* \[in\]  
调用方提供的 SNMP MIB 错误代码。

*pVal* \[out\]  
要接收指向包含该错误的文本说明的字符串的指针的调用方提供的位置。

<a name="return-value"></a>返回值
------------

此外可以返回 Win32 错误代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>S_OK</strong></td>
<td><p>操作成功。</p></td>
</tr>
<tr class="even">
<td><strong>E_POINTER</strong></td>
<td><p>无效<em>pVal</em>指针。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

```vb
Dim objPrinter, MIBErrorCode, MIBErrorString
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
...
' Get error code from MIB.
...
MIBErrorString = objPrinter.MibErrorDscp(ErrorCodeMIB)
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td>桌面设备</td>
</tr>
</tbody>
</table>
