---
title: Iasphelp get\_社区方法
description: 社区属性启用 ASP 网页，以获取打印服务器的简单网络管理协议 (SNMP) 团体名称。
MS-HAID:
- webfnc\_1d85e932-6de7-468a-b1dd-8a5678c65615.xml
- print.iasphelp\_community
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 39e8dff6-9eaf-43dd-b8ca-46982f3eae18
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
ms.openlocfilehash: ecf5783315979561f9d4a097f4580dde8f3dfa94
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544567"
---
# <a name="iasphelpgetcommunity-method"></a>Iasphelp::get\_社区方法

**社区**属性启用 ASP 网页，以获取打印服务器的简单网络管理协议 (SNMP) 团体名称。

<a name="syntax"></a>语法
------

```cpp
HRESULT get_Community(
  [out] BSTR *pVal
);
```

<a name="parameters"></a>参数
----------

*pVal* \[out\]  
调用方提供指向用于接收指向社区名称字符串的指针的位置。

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

如果打印机不支持通过 TCP/IP 端口监视器，则返回的字符串为空。

[ **Iasphelp::Open** ](iasphelp-open.md)前必须调用方法**Iasphelp::Community**属性可以进行查询。

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
<td>桌面设备</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅

[**Iasphelp::Open**](iasphelp-open.md)
