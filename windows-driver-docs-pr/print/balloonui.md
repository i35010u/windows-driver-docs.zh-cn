---
title: balloonUI 元素
description: 可选的 balloonUI 元素用于在客户端计算机上显示消息气球。
ms.assetid: 8db15dcb-26ed-429e-ad4c-e5dc59f9bbca
keywords:
- balloonUI 元素打印设备
topic_type:
- apiref
api_name:
- balloonUI
api_type:
- Schema
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1060ff4c5fe05e58752cee97e97f953b28f14992
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652933"
---
# <a name="balloonui-element"></a>balloonUI 元素

可选的**balloonUI**元素用于在客户端计算机上显示消息气球。

**BalloonUI**元素在*asyncui*命名空间中定义，此 URI 为： [https://schemas.microsoft.com/2003/print/asyncui/v1/request](https://schemas.microsoft.com/2003/print/asyncui/v1/request) （此资源可能在某些语言和国家/地区不可用。）

## <a name="usage"></a>Usage

```xml
<balloonUI
  iconID = "xs:string"
  resourceDll = "xs:string">
  child elements
</balloonUI>
```

## <a name="attributes"></a>属性

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
<td><p><strong>iconID</strong></p></td>
<td><p>xs:string</p></td>
<td><p>无</p></td>
<td><p></p>
<p>可选属性，指定在事件通知消息中显示的打印机图标。 特性值指定资源 DLL 中的图标的位置。 图标的大小必须为 32 x 32 像素，并具有任何颜色深度。</p></td>
</tr>
<tr class="even">
<td><p><strong>resourceDll</strong></p></td>
<td><p>xs:string</p></td>
<td><p>无</p></td>
<td><p></p>
<p>一个可选属性，指定包含要在事件通知消息中显示的打印机图标的资源 DLL。 此 DLL 应是打印机驱动程序的依赖文件，并且必须位于驱动程序资源文件夹中（例如，%SYSTEMROOT%\system32\spool\drivers\w32x86\3）。</p></td>
</tr>
</tbody>
</table>

## <a name="child-elements"></a>子元素

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
<td><p><a href="body.md" data-raw-source="[&lt;strong&gt;body&lt;/strong&gt;](body.md)"><strong>body</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，它提供在事件通知消息中显示的文本。 此文本应提供有关打印机事件的用户特定详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="title.md" data-raw-source="[&lt;strong&gt;title&lt;/strong&gt;](title.md)"><strong>词首</strong></a></p></td>
<td><p></p>
<p>一个必需的元素，该元素提供在事件通知消息标题中显示的文本。</p></td>
</tr>
</tbody>
</table>

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
<td><p><a href="requestopen.md" data-raw-source="[&lt;strong&gt;requestOpen&lt;/strong&gt;](requestopen.md)"><strong>requestOpen</strong></a></p></td>
<td><p></p>
<p>用于在客户端计算机上打开事件通知消息的元素。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

如果未指定属性**iconID**和**resourceDll** ，则会在气球消息中显示一般的打印机图标。 若要显示自定义打印机图标，请指定这两个属性的值。

## <a name="examples"></a>示例

下面的代码示例演示如何使用交互式气球将**CDATA**类型数据传递到 DLL。

```xml
<?xml version="1.0" ?> 
  <asyncPrintUIRequest xmlns="https://schemas.microsoft.com/2003/print/asyncui/v1/request">
    <v1>
      <requestOpen>
        <balloonUI iconID="1" resourceDll="IHV.dll">
          <title stringID="1234" resourceDll="IHV.dll" />
          <body stringID="100" resourceDll="IHV.dll">
            <parameter stringID="<5>" />
            <parameter stringID="1002" resourceDll="IHV.dll" />
          </body>
          <action dll="adc.dll" entrypoint="def" />
            IHV Data to pass into dll
            MUST BE CDATA
          </action>
        </balloonUI>
      </requestOpen>
    </v1>
  </asyncPrintUIRequest>
```

## <a name="see-also"></a>另请参阅

[**action**](action.md)

[**body**](body.md)

[**requestOpen**](requestopen.md)

[**词首**](title.md)
