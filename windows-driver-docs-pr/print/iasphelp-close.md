---
title: Iasphelp Close 方法
description: Close 方法使 ASP 网页能够关闭对打印机的访问。
MS-HAID:
- webfnc\_62b91ac5-2f01-44d6-9289-ee2136acacc4.xml
- print.iasphelp\_close
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- 关闭方法打印设备
- 关闭方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，Close 方法
topic_type:
- apiref
api_name:
- Iasphelp.Close
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed845974209e5e9cfc259d7583dac56c19285a5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796829"
---
# <a name="iasphelpclose-method"></a>Iasphelp：： Close 方法


**Close** 方法使 ASP 网页能够关闭对打印机的访问。

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

返回值始终为 \_ "正常"。


## <a name="vbscript-example"></a>VBScript 示例

必须已在先前对 [**Iasphelp：： Open**](iasphelp-open.md) 方法的调用中指定要关闭的打印机的名称。

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
<td>台式机</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅

[**Iasphelp：： Open**](iasphelp-open.md)
