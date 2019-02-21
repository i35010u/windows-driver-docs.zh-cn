---
title: Iasphelp get\_ComputerName 方法
description: ComputerName 属性启用 ASP 网页，若要获取打印服务器的名称。
MS-HAID:
- webfnc\_fd5c59b9-c223-4762-898d-693e9960619c.xml
- print.iasphelp\_computername
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 20fbd286-5b09-4c30-ae6c-4245854bc7b3
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
ms.openlocfilehash: b8f62d992c2123c5e3cbcb6df40c559ceba78a20
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525095"
---
# <a name="iasphelpgetcomputername-method"></a>Iasphelp::get\_ComputerName 方法

**ComputerName**属性启用 ASP 网页，若要获取打印服务器的名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_ComputerName(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
调用方提供指向用于接收指向计算机名称字符串的指针的位置。

<a name="return-value"></a>返回值
------------

此方法可以返回下列值之一。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>
