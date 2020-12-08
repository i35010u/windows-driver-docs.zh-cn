---
title: Iasphelp get \_ MibErrorDscp 方法
description: 使用 MibErrorDscp 属性，ASP 网页可以将简单的网络管理协议 (SNMP) 管理信息基本 (MIB) 错误代码转换为错误的文本说明。
MS-HAID:
- webfnc\_3931fbc6-1960-4d40-a6e3-8816ee832c89.xml
- print.iasphelp\_miberrordscp
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: 7ef6af7481be2ff5a09eafacdb680905bc04c8f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796801"
---
# <a name="iasphelpget_miberrordscp-method"></a>Iasphelp：： get \_ MibErrorDscp 方法

使用 **MibErrorDscp** 属性，ASP 网页可以将简单的网络管理协议 (SNMP) 管理信息基本 (MIB) 错误代码转换为错误的文本说明。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_MibErrorDscp(
  [in]  DWORD dwError,
  [out] BSTR  *pVal
);
```

<a name="parameters"></a>参数
----------

*dwError* \[中\]  
调用方提供的 SNMP MIB 错误代码。

*pVal* \[弄\]  
调用方提供的位置，用于接收指向字符串的指针，该字符串包含错误的文本说明。

<a name="return-value"></a>返回值
------------

也可以返回 Win32 错误代码。

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
<td><p><em>PVal</em>指针无效。</p></td>
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
<td>台式机</td>
</tr>
</tbody>
</table>
