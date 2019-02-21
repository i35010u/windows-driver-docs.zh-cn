---
title: action 元素
description: 可选的操作元素描述在用户单击气球消息中的按钮时将完成的操作。
ms.assetid: dae207ad-072e-4de6-b6a2-f1188ce91065
keywords:
- action 元素打印设备
topic_type:
- apiref
api_name:
- action
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e144aa68c24dd78cc398eeba7c6872bb95891a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522144"
---
# <a name="action-element"></a>action 元素


可选**操作**元素描述在用户单击气球消息中的按钮时将完成的操作。

**操作**中定义元素*asyncui*此 URI 处的命名空间： http://schemas.microsoft.com/2003/print/asyncui/v1/request。 （此资源可能不会在某些语言和国家/地区中可用。）

<a name="usage"></a>用法
-----

```xml
<action
  dll = "xs:string"
  entrypoint = "xs:string">
  text
</action>
```

<a name="attributes"></a>属性
----------

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
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>dll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>指定的 DLL，由 IHV，包含当用户单击按钮时要调用的函数提供的必需的属性。</p></td>
</tr>
<tr class="even">
<td><p><strong>entrypoint</strong></p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p></p>
<p>由 IHV 提供在 DLL 中指定要调用的函数的必需的属性。 此函数应返回<strong>NULL</strong>时调用。</p></td>
</tr>
</tbody>
</table>

<a name="text-value"></a>文本值
----------

可选的字符串，格式为 CDATA、 要传递给驱动程序资源 DLL。

## <a name="child-elements"></a>子元素


没有子元素。

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
<p>提供的文本显示在事件通知消息。 此文本应提供用户有关打印机事件的特定详细信息。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

**操作**元素用于交互式提示框中，这是类似于正则气球，但它包括一个用于用户单击的按钮。

<a name="examples"></a>示例
--------

下面的 XML 代码示例将运行*IHV.exe*客户端计算机上的程序

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

下面的代码示例演示如何使用**操作**元素将数据传递给资源 DLL。

```xml
<?xml version="1.0" ?>
   <asyncPrintUIRequest
    xmlns="http://schemas.microsoft.com/2003/print/asyncui/v1/request">
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

## <a name="see-also"></a>另请参阅


[**balloonUI**](balloonui.md)

 

 




