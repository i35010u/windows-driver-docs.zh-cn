---
title: action 元素
description: 可选操作元素描述当用户单击气球消息中的按钮时将完成的操作。
keywords:
- 操作元素打印设备
topic_type:
- apiref
api_name:
- action
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26991d7b1a9002a60435c691e6b5cf7053866271
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794245"
---
# <a name="action-element"></a>action 元素

可选 **操作** 元素描述当用户单击气球消息中的按钮时将完成的操作。

**操作** 元素在此 URI 的 *asyncui* 命名空间中定义：

```xml
https://schemas.microsoft.com/2003/print/asyncui/v1/request
```

此资源可能在某些语言和国家/地区不可用。

## <a name="usage"></a>使用情况

```xml
<action
  dll = "xs:string"
  entrypoint = "xs:string">
  text
</action>
```

## <a name="attributes"></a>特性

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>.dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，它指定由 IHV 提供的 DLL，其中包含当用户单击按钮时要调用的函数。</p></td>
</tr>
<tr class="even">
<td><p><strong>入口</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>一个必需的属性，该属性指定在由 IHV 提供的 DLL 中调用的函数。 调用时，此函数应返回 <strong>NULL</strong> 。</p></td>
</tr>
</tbody>
</table>

## <a name="text-value"></a>文本值

要传递给驱动程序资源 DLL 的可选字符串，格式为 CDATA。

## <a name="child-elements"></a>子元素

没有任何子元素。

## <a name="parent-elements"></a>父元素

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="balloonui.md" data-raw-source="[&lt;strong&gt;balloonUI&lt;/strong&gt;](balloonui.md)"><strong>balloonUI</strong></a></p></td>
<td><p></p>
<p>提供事件通知消息中显示的文本。 此文本应提供有关打印机事件的用户特定详细信息。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

**操作** 元素与一个交互式气球一起使用，它与常规气球类似，但它包含一个按钮，用户单击该按钮即可。

## <a name="examples"></a>示例

以下 XML 代码示例将在客户端计算机上运行 *IHV.exe* 程序。

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="<5>" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

下面的代码示例演示如何使用 **action** 元素向资源 DLL 传递数据。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll"/>
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="<5>" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
          <action dll="adc.dll" entrypoint="def" >
            IHV CDATA to pass into the resource DLL
          </action>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>请参阅

[**balloonUI**](balloonui.md)
