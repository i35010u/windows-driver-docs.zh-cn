---
title: 输出关键字
description: 这些关键字用于描述给定 3D 生产作业的实际输出进程。
ms.assetid: FBCE5E9C-8411-46C1-899E-A6C8FE27D947
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80c190b112862a9068f9ef8e5c067f1b8f12c905
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324763"
---
# <a name="output-keywords"></a>输出关键字


这些关键字用于描述给定 3D 生产作业的实际输出进程。

## <a name="41-job3dquality"></a>4.1. Job3DQuality


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特征</th>
<th>详细信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名称</td>
<td>psk3d:Job3DQuality</td>
</tr>
<tr class="even">
<td>对有效</td>
<td><p>PrintCapabilities 文档</p>
<p>PrintTicket 文档</p></td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>功能</td>
</tr>
<tr class="even">
<td>SelectionType</td>
<td>psk:PickOne</td>
</tr>
<tr class="odd">
<td>目录</td>
<td><p>选项定义的三维制造的打印架构关键字如下所示：</p>
<p><strong>子项：</strong>Option psk3d:Draft</p>
<p><strong>描述:</strong>此选项指定设备应该已使用设备的最低分辨率最快的输出。</p>
<p><strong>子项：</strong>选项 psk3d:Medium</p>
<p><strong>描述:</strong>此选项指定设备应提供相等的优先级来输出和输出分辨率的速度。</p>
<p><strong>子项：</strong>选项 psk3d:High</p>
<p><strong>描述:</strong>此选项指定设备，应为最高优先级提供输出分辨率，而不考虑速度。</p></td>
</tr>
</tbody>
</table>

 

Job3DQuality 关键字的用法

```xml
<psf:Feature name="psk3d:Job3DQuality">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:Draft" />
    <psf:Option name="psk3d:Medium" />
    <psf:Option name="psk3d:High" />
</psf:Feature>
```

## <a name="42-job3ddensity"></a>4.2. Job3DDensity


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特征</th>
<th>详细信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名称</td>
<td>psk3d:Job3DDensity</td>
</tr>
<tr class="even">
<td>对有效</td>
<td><p>PrintCapabilities 文档</p>
<p>PrintTicket 文档</p></td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>功能</td>
</tr>
<tr class="even">
<td>SelectionType</td>
<td>psk:PickOne</td>
</tr>
<tr class="odd">
<td>目录</td>
<td><p>选项定义的三维制造的打印架构关键字如下所示：</p>
<p><strong>子项：</strong>选项 psk3d:Hollow</p>
<p><strong>描述:</strong>此选项指定设备应输出包含没有内部支持 （空白） 的作业。</p>
<p><strong>子项：</strong>选项 psk3d:Low</p>
<p><strong>描述:</strong>此选项指定设备应输出具有大约 10 %infill 支持的作业。</p>
<p><strong>子项：</strong>选项 psk3d:Medium</p>
<p><strong>描述:</strong>此选项指定设备应输出具有大约 25 %infill 支持的作业。</p>
<p><strong>子项：</strong>选项 psk3d:High</p>
<p><strong>描述:</strong>此选项指定设备应输出具有大约 50 %infill 支持的作业。</p>
<p><strong>子项：</strong>Option psk3d:Solid</p>
<p><strong>描述:</strong>此选项指定应输出设备作业 100%填充。</p></td>
</tr>
</tbody>
</table>

 

Job3DDensity 关键字的用法

```xml
<psf:Feature name="psk3d:Job3DDensity">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:Hollow"/>
    <psf:Option name="psk3d:Low"/>
    <psf:Option name="psk3d:Medium"/>
    <psf:Option name="psk3d:High"/>
    <psf:Option name="psk3d:Solid"/>
</psf:Feature>
```

## <a name="43-job3dsliceheight"></a>4.3. Job3DSliceHeight


此参数应进行通信所需的每个切片，粗细在 psk3d:Job3DQuality 参数被视为不足。

Job3DSliceHeight 关键字配置文件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特征</th>
<th>详细信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名称</td>
<td>psk3d:Job3DSliceHeight</td>
</tr>
<tr class="even">
<td>对有效</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterDef</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>psk3d:Job3DSliceHeight 是 IntegerParamType §2.1.3.1 中, 所述"&lt;psf:ParameterDef&gt;"打印架构规范中。</p>
<p><strong>子项：</strong>IntegerParamType</p>
<p><strong>描述:</strong></p>
<p>Psf:MinValue 属性值必须是大于 0。</p>
<p>Psf:MaxValue 属性值可能由供应商定义，必须是大于或等于 psf:MinValue 属性值。</p>
<p>Psf:Multiple 属性值必须为 1。</p>
<p>Psf:Multiple 属性值必须为 1。</p>
<p>属性值必须 psf:UnitType 是微米。</p></td>
</tr>
</tbody>
</table>

 

Job3DSliceHeight 初始化配置文件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特征</th>
<th>详细信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名称</td>
<td>psk3d:Job3DSliceHeight</td>
</tr>
<tr class="even">
<td>对有效</td>
<td>PrintTicket 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterInit</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>包含 1&lt;值&gt;子元素，如下所示：</p>
<p><strong>子项：</strong>ReplTest1</p>
<p><strong>xsi: type:</strong> xsd: integer</p>
<p><strong>值：</strong>SliceHeight</p>
<p><strong>描述:</strong>SliceHeight 必须包含一个等于微米所需扇区高度的正整数。</p></td>
</tr>
</tbody>
</table>

 

Job3DSliceHeight 关键字的用法

参数定义如下所示：

```xml
<psf:ParameterDef name="psk3d:Job3DSliceHeight">
    <psf:Property name="psf:DataType">
        <psf:Value xsi:type="xsd:QName">xsd:integer</psf:Value>
    </psf:Property>
    <psf:Property name="psf:DefaultValue">
        <psf:Value xsi:type="xsd:integer">100</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MaxValue">
        <psf:Value xsi:type="xsd:integer">3000</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MinValue">
        <psf:Value xsi:type="xsd:integer">50</psf:Value>
    </psf:Property>
    <psf:Property name="psf:Multiple">
        <psf:Value xsi:type="xsd:integer">1</psf:Value>
    </psf:Property>
    <psf:Property name="psf:Mandatory">
        <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
    </psf:Property>
    <psf:Property name="psf:UnitType">
        <psf:Value xsi:type="xsd:string">microns</psf:Value>
    </psf:Property>
</psf:ParameterDef>
```

此参数进行初始化，如下所示：

```xml
<psf:ParameterInit name="psk3d:Job3DSliceHeight">
    <psf:Value xsi:type="xsd:integer">150</psf:Value>
</psf:ParameterInit>
```

## <a name="44-job3doutputcolor"></a>4.4. Job3DOutputColor


Psk3d:Job3DOutputColor 关键字指定模型是否要在完整的颜色或使用一种单色材料 （基材料的颜色），可重现。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>特征</th>
<th>详细信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>名称</td>
<td>psk3d:Job3DOutputColor</td>
</tr>
<tr class="even">
<td>对有效</td>
<td><p>PrintCapabilities 文档</p>
<p>PrintTicket 文档</p></td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>功能</td>
</tr>
<tr class="even">
<td>SelectionType</td>
<td>psk:PickOne</td>
</tr>
<tr class="odd">
<td>目录</td>
<td><p>选项定义的三维制造的打印架构关键字如下所示：</p>
<p><strong>子项：</strong>Option psk3d:Color</p>
<p><strong>描述:</strong>此选项指定设备应输出中全彩色的作业。</p>
<p><strong>子项：</strong>选项 psk3d:Monochrome</p>
<p><strong>描述:</strong>此选项指定设备应输出中一种颜色的作业。</p></td>
</tr>
</tbody>
</table>

 

Job3DOutputColor 关键字的用法

```xml
<psf:Feature name="psk3d:Job3DOutputColor">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:Color" />
    <psf:Option name="psk3d:Monochrome" />
</psf:Feature>
```

 

 




