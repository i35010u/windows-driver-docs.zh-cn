---
title: Iasphelp get\_PaperNames 方法
description: PaperNames 属性启用 ASP 网页，以获取一组命名的打印机的纸张的所有窗体的字符串。
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
ms.openlocfilehash: 3efc5f51ea2aad42977eb26e6da0354232e7225e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357235"
---
# <a name="iasphelpgetpapernames-method"></a>Iasphelp::get\_PaperNames 方法

**PaperNames**属性启用 ASP 网页，以获取一组命名的打印机的纸张的所有窗体的字符串。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_PaperNames(
  [out] VARIANT *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
要接收到一组表示打印机的所有纸张窗体的字符串的指针的调用方提供的位置。

<a name="return-value"></a>返回值
------------

下表中，此属性返回的值之一。

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

此属性的处理程序通过调用在打印机驱动程序获取的纸质表单列表[ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)函数与 DC\_PAPERNAMES 标志设置。

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::PaperNames**属性可以进行查询。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)

[**Iasphelp::Open**](iasphelp-open.md)
