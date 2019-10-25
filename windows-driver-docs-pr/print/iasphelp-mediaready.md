---
title: Iasphelp get\_MediaReady 方法
description: 使用 MediaReady 属性可以获取一组字符串，这些字符串命名当前可供使用的打印机的所有纸张窗体。
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
ms.openlocfilehash: 99dd80c0fb7807f0d820d06f4f71734444653cff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838095"
---
# <a name="iasphelpget_mediaready-method"></a>Iasphelp：： get\_MediaReady 方法

使用**MediaReady**属性可以获取一组字符串，这些字符串命名当前可供使用的打印机的所有纸张窗体。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_MediaReady(
  [out] VARIANT *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
调用方提供的位置，用于接收指向一组字符串的指针，这些字符串命名当前可供使用的打印机的所有纸张窗体。

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
<td><p>未调用<a href="iasphelp-open.md" data-raw-source="[&lt;strong&gt;Iasphelp::Open&lt;/strong&gt;](iasphelp-open.md)"><strong>Iasphelp：： Open</strong></a>方法。</p></td>
</tr>
<tr class="odd">
<td><strong>E_OUTOFMEMORY</strong></td>
<td><p>内存不足。</p></td>
</tr>
</tbody>
</table>

## <a name="vbscript-example"></a>VBScript 示例

此方法获取当前可供使用的纸张窗体的列表，该列表通过在设置了 DC\_MEDIAREADY 标志的情况下调用打印机驱动程序的[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)函数。

在查询**Iasphelp：： MediaReady**属性之前，必须先调用[**Iasphelp：： Open**](iasphelp-open.md)方法。

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
<td>桌面</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**DrvDeviceCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicecapabilities)

[**Iasphelp：： Open**](iasphelp-open.md)
