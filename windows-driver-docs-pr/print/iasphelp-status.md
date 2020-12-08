---
title: Iasphelp 获取 \_ 状态方法
description: "\"状态\" 属性允许 ASP 网页确定打印机状态。"
MS-HAID:
- webfnc\_30feffa7-1aa0-4b66-9d0a-1f66025272c3.xml
- print.iasphelp\_status
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
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
ms.openlocfilehash: 5125f3090ca97205c9f1eb17f0241a34f9163206
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835735"
---
# <a name="iasphelpget_status-method"></a>Iasphelp：： get \_ Status 方法

" **状态** " 属性允许 ASP 网页确定打印机状态。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_Status(
  [out] long *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的指向接收打印机状态标志的位置的指针。 有关更多信息，请参见下面的“备注”部分。

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
<td><strong>E_HANDLE</strong></td>
<td><p>未调用 <a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"><strong>Iasphelp：： Open</strong></a> 方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

属性值是打印机状态代码，它是0，或者是 \_ \_ *XXX* 在标头文件 Winspool.drv 中为 **Status** 打印机 \_ 信息 \_ 2 结构的状态成员定义的一个或多个打印机状态 XXX 标志的按位 "或"。 有关此结构的详细信息，请参阅 Windows SDK 文档。

必须先调用 [**Iasphelp：： Open**](iasphelp-open.md) 方法，然后才能查询 **Iasphelp：： Status** 属性。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：： Open**](iasphelp-open.md)
