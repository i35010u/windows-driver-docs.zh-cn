---
title: Iasphelp get\_LongPaperName 方法
description: LongPaperName 属性启用 ASP 网页，若要将短纸张名称转换为长纸张名称。
MS-HAID:
- webfnc\_17250b54-29f4-41c5-bdf2-b72e0823d8e4.xml
- print.iasphelp\_longpapername
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 14e6d6db-c429-4d80-840b-c4e0102c9380
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
ms.openlocfilehash: cda3f8b569ca82bcdef8892db983e07b7b0feb78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392855"
---
# <a name="iasphelpgetlongpapername-method"></a>Iasphelp::get\_LongPaperName 方法

**LongPaperName**属性启用 ASP 网页，若要将短纸张名称转换为长纸张名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_LongPaperName(
  [in]  BSTR bstrShortName,
  [out] BSTR *pVal
);
```

<a name="parameters"></a>Parameters
----------

*bstrShortName* \[in\]  
指向包含短纸张名称的字符串的调用方提供的指针。

*pVal* \[out\]  
调用方提供的位置，用于接收指向包含长纸张名称的字符串。

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
<td><p>在至少一个参数不指向有效内存位置。</p></td>
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
<td>桌面设备</td>
</tr>
</tbody>
</table>
