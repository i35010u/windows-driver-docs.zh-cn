---
title: Iasphelp Close 方法
description: Close 方法启用 ASP 网页，以关闭到打印机的访问。
MS-HAID:
- webfnc\_62b91ac5-2f01-44d6-9289-ee2136acacc4.xml
- print.iasphelp\_close
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 45457eb9-a791-450f-b3fd-f4e7dabc7a70
keywords:
- Close 方法打印设备
- Close 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，Close 方法
topic_type:
- apiref
api_name:
- Iasphelp.Close
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03d93d60dc290f9541bd404847dea130bbb07c49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542989"
---
# <a name="iasphelpclose-method"></a>Iasphelp::Close 方法


**关闭**方法启用 ASP 网页，以关闭到打印机的访问。

<a name="syntax"></a>语法
------

```cpp
HRESULT Close();
```

<a name="parameters"></a>参数
----------

此方法没有任何参数。

<a name="return-value"></a>返回值
------------

返回值始终为 S\_确定。


## <a name="vbscript-example"></a>VBScript 示例

正在关闭打印机的名称必须对上一个调用中指定[ **Iasphelp::Open** ](iasphelp-open.md)方法。

```vb
Dim objPrinter
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
...
objPrinter.Close
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

## <a name="see-also"></a>另请参阅

[**Iasphelp::Open**](iasphelp-open.md)
