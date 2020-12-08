---
title: Iasphelp 获取 \_ ComputerName 方法
description: ComputerName 属性允许 ASP 网页获取打印服务器的名称。
MS-HAID:
- webfnc\_fd5c59b9-c223-4762-898d-693e9960619c.xml
- print.iasphelp\_computername
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_ComputerName 方法打印设备
- get_ComputerName 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_ComputerName 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_ComputerName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc0157e1e91fdfdbb43f7c7d9e29fed07294e944
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835795"
---
# <a name="iasphelpget_computername-method"></a>Iasphelp：：获取 \_ ComputerName 方法

**ComputerName** 属性允许 ASP 网页获取打印服务器的名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_ComputerName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向接收指向计算机名称字符串的指针的位置的指针。

<a name="return-value"></a>返回值
------------

此方法可以返回这些值之一。

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
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

```vb
Dim objPrinter, CompName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
CompName = objPrinter.ComputerName
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
