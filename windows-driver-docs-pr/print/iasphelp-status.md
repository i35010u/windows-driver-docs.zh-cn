---
title: Iasphelp get\_状态方法
description: Status 属性启用 ASP 网页，以确定打印机状态。
MS-HAID:
- webfnc\_30feffa7-1aa0-4b66-9d0a-1f66025272c3.xml
- print.iasphelp\_status
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: cff9dd7d-722b-4917-84ca-d6b17e8e64a4
keywords:
- get_Status 方法打印设备
- get_Status 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_Status 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_Status
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69bd9d6bbf5284ec1676acafc7677186caf2b19b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341330"
---
# <a name="iasphelpgetstatus-method"></a>Iasphelp::get\_状态方法

**状态**属性启用 ASP 网页，以确定打印机状态。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_Status(
  [out] long *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
调用方提供指向用于接收打印机状态标志的位置。 有关详细信息，请参阅以下备注部分。

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
<td><strong>E_HANDLE</strong></td>
<td><p><a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"> <strong>Iasphelp::Open</strong> </a>尚未调用方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

属性值是 0 或一个或多个打印机的按位 OR 打印机状态代码\_状态\_*XXX*标头中定义的标记文件的 Winspool.h**状态**成员的打印机\_信息\_2 结构。 有关此结构的详细信息，请参阅 Windows SDK 文档。

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::Status**属性可以进行查询。

```vb
Dim objPrinter, PtrStatus
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PtrStatus = objPrinter.Status
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

## <a name="see-also"></a>请参阅

[**Iasphelp::Open**](iasphelp-open.md)
