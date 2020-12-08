---
title: Iasphelp 获取 \_ 社区方法
description: 使用社区属性，ASP 网页可以 (SNMP) 社区名称获取打印服务器的简单网络管理协议。
MS-HAID:
- webfnc\_1d85e932-6de7-468a-b1dd-8a5678c65615.xml
- print.iasphelp\_community
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
keywords:
- get_Community 方法打印设备
- get_Community 方法打印设备，Iasphelp 接口
- Iasphelp 接口打印设备，get_Community 方法
topic_type:
- apiref
api_name:
- Iasphelp.get_Community
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20ae66cf9b748bc2358f5c1fe453e5a2da0236d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796825"
---
# <a name="iasphelpget_community-method"></a>Iasphelp：： get \_ 团体方法

使用 **社区** 属性，ASP 网页可以 (SNMP) 社区名称获取打印服务器的简单网络管理协议。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_Community(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[弄\]  
调用方提供的用于接收指向团体名称字符串的指针的位置的指针。

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

如果 TCP/IP 端口监视器不支持打印机，则返回的字符串为空。

在查询 **Iasphelp：：社团** 属性之前，必须先调用 [**Iasphelp：： Open**](iasphelp-open.md)方法。

```vb
Dim objPrinter, CommName
strPrinter = Session("MS_printer")
Set objPrinter = Server.CreateObject ("OlePrn.AspHelp")
objPrinter.Open strPrinter
CommName = objPrinter.Community
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
