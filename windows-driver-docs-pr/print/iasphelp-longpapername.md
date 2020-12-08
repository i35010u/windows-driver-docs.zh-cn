---
title: Iasphelp get \_ LongPaperName 方法
description: 使用 LongPaperName 属性，ASP 网页可以将短的纸张名称转换为长的纸张名称。
MS-HAID:
- webfnc\_17250b54-29f4-41c5-bdf2-b72e0823d8e4.xml
- print.iasphelp\_longpapername
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_LongPaperName 方法打印设备
- get_LongPaperName 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_LongPaperName 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_LongPaperName
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3374e82017e72fe0934c4d7e0cbe275cbf246e60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796804"
---
# <a name="iasphelpget_longpapername-method"></a>Iasphelp：： get \_ LongPaperName 方法

使用 **LongPaperName** 属性，ASP 网页可以将短的纸张名称转换为长的纸张名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_LongPaperName(
  [in]  BSTR bstrShortName,
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*bstrShortName* \[中\]  
调用方提供的指向包含短文件名的字符串的指针。

*pVal* \[弄\]  
调用方提供的位置，用于接收指向包含长文件名的字符串的指针。

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
<td><p>至少一个参数不指向有效的内存位置。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

```vb
Dim objPrinter, LongName
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
LongName = objPrinter.LongPaperName("iso-a0")
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
