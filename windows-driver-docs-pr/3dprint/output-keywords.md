---
title: 输出关键字
description: 这些关键字用于描述给定3D 制造作业的实际输出过程。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4736b2c136eee4e442737ef918fc2ce6550ea3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788119"
---
# <a name="output-keywords"></a>输出关键字


这些关键字用于描述给定3D 制造作业的实际输出过程。

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
<td>适用于</td>
<td><p>PrintCapabilities 文档</p>
<p>PrintTicket 文档</p></td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>功能</td>
</tr>
<tr class="even">
<td>SelectionType</td>
<td>psk： PickOne</td>
</tr>
<tr class="odd">
<td>目录</td>
<td><p>用于3D 制造的打印架构关键字定义的选项如下所示：</p>
<p><strong>子级：</strong> 选项 psk3d：草稿</p>
<p><strong>说明：</strong> 此选项指定设备的输出速度最快，设备的分辨率可能最低。</p>
<p><strong>子级：</strong> 选项 psk3d：中型</p>
<p><strong>说明：</strong> 此选项指定设备应为输出和输出分辨率的速度给予相同的优先级。</p>
<p><strong>子级：</strong> 选项 psk3d：高</p>
<p><strong>说明：</strong> 此选项指定设备应为输出分辨率指定最高优先级，而不考虑速度。</p></td>
</tr>
</tbody>
</table>

 

Job3DQuality 关键字用法

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
<td>适用于</td>
<td><p>PrintCapabilities 文档</p>
<p>PrintTicket 文档</p></td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>功能</td>
</tr>
<tr class="even">
<td>SelectionType</td>
<td>psk： PickOne</td>
</tr>
<tr class="odd">
<td>目录</td>
<td><p>用于3D 制造的打印架构关键字定义的选项如下所示：</p>
<p><strong>子级：</strong> 选项 psk3d：中空</p>
<p><strong>说明：</strong> 此选项指定设备在没有内部的情况下输出作业支持 (中空) 。</p>
<p><strong>子级：</strong> 选项 psk3d：低</p>
<p><strong>说明：</strong> 此选项指定设备应输出具有大约 10% infill 支持的作业。</p>
<p><strong>子级：</strong> 选项 psk3d：中型</p>
<p><strong>说明：</strong> 此选项指定设备应输出大约 25% infill 支持的作业。</p>
<p><strong>子级：</strong> 选项 psk3d：高</p>
<p><strong>说明：</strong> 此选项指定设备应输出具有大约 50% infill 支持的作业。</p>
<p><strong>子级：</strong> 选项 psk3d：固态</p>
<p><strong>说明：</strong> 此选项指定设备应输出作业100%。</p></td>
</tr>
</tbody>
</table>

 

Job3DDensity 关键字用法

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


如果 psk3d： Job3DQuality 参数被视为不足，则应使用此参数来传达每个切片所需的宽度。

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
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterDef</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>psk3d： Job3DSliceHeight 是一种 IntegerParamType，如 "打印架构" 规范的第 2.1.3.1 " &lt; psf： ParameterDef" 中所述 &gt; 。</p>
<p><strong>子级：</strong> IntegerParamType</p>
<p><strong>描述：</strong></p>
<p>Psf： MinValue 属性值必须大于0。</p>
<p>Psf：属性值可由供应商定义，且必须大于或等于 psf： MinValue 属性值。</p>
<p>Psf：多个属性值必须为1。</p>
<p>Psf：多个属性值必须为1。</p>
<p>Psf： Unittype.pixel 度量属性值必须为 microns。</p></td>
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
<td>适用于</td>
<td>PrintTicket 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterInit</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>正好包含1个 &lt; 值 &gt; 子元素，如下所示：</p>
<p><strong>子级：</strong> 负值</p>
<p><strong>xsi： type：</strong> xsd： integer</p>
<p><strong>值：</strong> SliceHeight</p>
<p><strong>说明：</strong> SliceHeight 在 microns 中必须包含一个等于所需切片高度的正整数。</p></td>
</tr>
</tbody>
</table>

 

Job3DSliceHeight 关键字用法

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

此参数的初始化如下：

```xml
<psf:ParameterInit name="psk3d:Job3DSliceHeight">
    <psf:Value xsi:type="xsd:integer">150</psf:Value>
</psf:ParameterInit>
```

## <a name="44-job3doutputcolor"></a>4.4。 Job3DOutputColor


Psk3d： Job3DOutputColor 关键字指定是以完整颜色还是使用单个单色 (材料来重现模型) 基本材料的颜色。

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
<td>适用于</td>
<td><p>PrintCapabilities 文档</p>
<p>PrintTicket 文档</p></td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>功能</td>
</tr>
<tr class="even">
<td>SelectionType</td>
<td>psk： PickOne</td>
</tr>
<tr class="odd">
<td>目录</td>
<td><p>用于3D 制造的打印架构关键字定义的选项如下所示：</p>
<p><strong>子级：</strong> 选项 psk3d： Color</p>
<p><strong>说明：</strong> 此选项指定设备应以全色输出作业。</p>
<p><strong>子级：</strong> 选项 psk3d：单色</p>
<p><strong>说明：</strong> 此选项指定设备应以单色输出作业。</p></td>
</tr>
</tbody>
</table>

 

Job3DOutputColor 关键字用法

```xml
<psf:Feature name="psk3d:Job3DOutputColor">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:Color" />
    <psf:Option name="psk3d:Monochrome" />
</psf:Feature>
```

 

 




