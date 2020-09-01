---
title: Iasphelp get \_ PaperNames 方法
description: 使用 PaperNames 属性，ASP 网页可以获取一组命名打印机的所有纸张格式的字符串。
MS-HAID:
- webfnc\_be2b332f-6300-4b3e-9fa7-fd2fd0bdffe5.xml
- print.iasphelp\_papernames
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 558cf0a6-d98b-4d59-ae37-d19ced289bf0
keywords:
- get_PaperNames 方法打印设备
- get_PaperNames 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_PaperNames 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_PaperNames
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a40098a405e7c18540010a283e8593ef619788b9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205877"
---
# <a name="iasphelpget_papernames-method"></a>Iasphelp：： get \_ PaperNames 方法

使用 **PaperNames** 属性，ASP 网页可以获取一组命名打印机的所有纸张格式的字符串。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PaperNames(
  [out] VARIANT *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的位置，用于接收指向一组表示打印机的所有纸张窗体的字符串的指针。

<a name="return-value"></a>返回值
------------

此属性返回下表中的值之一。

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

此属性的处理程序通过在设置了 DC PAPERNAMES 标志的情况下调用打印机驱动程序的 [**DrvDeviceCapabilities**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities) 函数，获取纸张窗体的列表 \_ 。

在查询**Iasphelp：:P apernames**属性之前，必须先调用[**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
Dim objPrinter, PaperNameArray
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
PaperNameArray = objPrinter.PaperNames
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
<td>“桌面”</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**DrvDeviceCapabilities**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)

[**Iasphelp：： Open**](iasphelp-open.md)