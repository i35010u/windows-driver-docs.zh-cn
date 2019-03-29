---
title: Iasphelp get\_MediaReady 方法
description: MediaReady 属性启用 ASP 网页，以获取该名称是当前可供使用的打印机纸张的所有窗体的一组字符串。
MS-HAID:
- webfnc\_b10e8434-7e12-4bb5-8c43-77cb890f72a8.xml
- print.iasphelp\_mediaready
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1e90649a-6075-4b78-93fd-781c3e363b5f
keywords:
- get_MediaReady 方法打印设备
- get_MediaReady 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_MediaReady 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_MediaReady
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a5a7721ffeda339468e553b1d055218b6694fe0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567780"
---
# <a name="iasphelpgetmediaready-method"></a>Iasphelp::get\_MediaReady 方法

**MediaReady**属性启用 ASP 网页，以获取一组命名的打印机纸张窗体的所有当前可供使用的字符串。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_MediaReady(
  [out] VARIANT *pVal
);
```

<a name="parameters"></a>Parameters
----------

*pVal* \[out\]  
调用方提供的位置，以接收所有纸张的窗体的打印机的当前可使用该名称的一组字符串的指针。

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

此方法获取的纸质表单，通过调用打印机驱动程序的当前可供使用的名称的列表[ **DrvDeviceCapabilities** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicecapabilities)函数与 DC\_MEDIAREADY标志设置。

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::MediaReady**属性可以进行查询。

```vb
Dim objPrinter, MediaReadyArray
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
MediaReadyArray = objPrinter.MediaReady
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
