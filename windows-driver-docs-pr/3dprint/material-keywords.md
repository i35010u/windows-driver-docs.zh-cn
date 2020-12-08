---
title: 材料关键字
description: 这些关键字介绍了用于创建3D 对象的设备中的原始材料。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82d3bea0ffd3e85c9a6c18993e2469ee1cc506af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786601"
---
# <a name="material-keywords"></a>材料关键字


这些关键字介绍了用于创建3D 对象的设备中的原始材料。

## <a name="31-job3dmaterialcount"></a>3.1. Job3DMaterialCount


此参数必须定义设备中可用于单个作业的当前已加载材料的数量。 如果设备不知道加载物料的时间，则此参数必须是单个作业中使用的可能的材料数。 如果打印机只有单个未知材料，则可以省略此参数以及所有其他材料关键字。

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
<td>psk3d:Job3DMaterialCount</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>properties</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>正好包含1个 &lt; 值 &gt; 子元素，如下所示：</p>
<p><strong>子级：</strong> 负值</p>
<p><strong>xsi： type：</strong> xsd： integer</p>
<p><strong>值：</strong> JobMaterialCountText</p>
<p><strong>说明：</strong> JobMaterialCountText，如果指定了此属性，则必须包含一个正整数，用于标识此设备上可用的材料数。</p></td>
</tr>
</tbody>
</table>



Job3DMaterialCount 关键字用法

```cpp
<psf:Property name="psk3d:Job3DMaterialCount">
    <psf:Value xsi:type="xsd:integer">2</psf:Value>
</psf:Property>
```

## <a name="32-job3dmaterials"></a>3.2. Job3DMaterials


此属性必须包含设备中所加载材料的说明，如果这是未知的，则必须包含可能的位置材料的枚举。

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
<td>psk3d:Job3DMaterials</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>properties</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>包含一个或多个子属性元素，如下所示：</p>
<p><strong>子级：</strong> 属性列表</p>
<p><strong>xsi： type：</strong> 不适用</p>
<p><strong>值：</strong> MaterialsList</p>
<p><strong>说明：</strong> MaterialsList 包含一组子属性。</p></td>
</tr>
</tbody>
</table>



### <a name="321-materialslist-properties"></a>3.2.1. MaterialsList 属性

供应商必须创建自己的材料，并枚举其设备中加载的打印材料。 这些材料的名称是由供应商定义的，如果设备能够从已加载的材料墨盒读取此类信息，则应该代表股票说明。 如果设备不具有此信息，则供应商应将材料名称定义为描述此材料加载的位置 (例如，"Extruder" ) 。

每个材料应指定以下子属性。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>材料名称</th>
<th>xsi:type</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>psk： DisplayName</td>
<td>xsd:string</td>
<td>此属性应包含 psf： Value 元素，其中包含本地化的显示名称。</td>
</tr>
<tr class="even">
<td>psk3d:MaterialColor</td>
<td>xsd:string</td>
<td><p>设备可以定义此属性以指定材料的颜色。 如果指定此值，则该值必须是符合以下说明的 sRGB 颜色：</p>
<div class="code">
<code>cpp
sRGBColorText = "#" hR hG hB hA
hR = hG = hB = hA = hexpair
hexpair = hexdigit hexdigit
hexdigit = "0" / "1" / "2" / "3" /
           "4" / "5" / "6" / "7" /
           "8" / "9" / "A" / "B" /
           "C" / "D" / "E" / "F" /
           "a" / "b" / "c" / "d" /
           "e" / "f"</code>
</div>
<p>hR、hG、Hb-acct-wc 和 hA 分别指定了红色、绿色、蓝色和 alpha 分量的十六进制单字节值，范围从00到 FF。 设备可能会省略 alpha (例如 #hRhGhB) ，在这种情况下，alpha 将使用 FF 的默认值 (完全不透明的) 。</p></td>
</tr>
</tbody>
</table>



Job3DMaterials 关键字用法

```cpp
<psf:Property name="psk3d:Job3DMaterials">
    <psf:Property name="vnd:ABS_RED">
        <psf:Property name="psk:DisplayName">
            <psf:Value xsi:type="xsd:string">Red ABS Plastic</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:MaterialColor">
            <psf:Value xsi:type="xsd:string">#FF0000</psf:Value>
        </psf:Property>
    </psf:Property>
    <psf:Property name="vnd:PLA_TEAL">
        <psf:Property name="psk:DisplayName">
            <psf:Value xsi:type="xsd:string">Teal PLA Plastic</psf:Value>
        </psf:Property>
        <psf:Property name="psk3d:MaterialColor">
            <psf:Value xsi:type="xsd:string">#00FFFF</psf:Value>
        </psf:Property>
    </psf:Property>
</psf:Property>
```

## <a name="33-job3dsupports"></a>3.3. Job3DSupports


Psk3d： Job3DSupports 关键字指定此作业是否应包含设备或驱动程序生成的 *支持* 。

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
<td>psk3d:Job3DSupports</td>
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
<p><strong>子级：</strong> 选项 psk3d： SupportsIncluded</p>
<p><strong>说明：</strong> 此选项指定设备应为模型生成外部支持。</p>
<p><strong>子级：</strong> 选项 psk3d： SupportsExcluded</p>
<p><strong>说明：</strong> 此选项指定设备不应为模型生成外部支持。</p></td>
</tr>
</tbody>
</table>



Job3DSupports 关键字用法

```cpp
<psf:Feature name="psk3d:Job3DSupports">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:SupportsIncluded" />
    <psf:Option name="psk3d:SupportsExcluded" />
</psf:Feature>
```

### <a name="331-job3dsupportsmaterial"></a>3.3.1. Job3DSupportsMaterial

如果选择了选项 psk3d： SupportsIncluded，并且设备支持多个材料，则此参数应指示用于支持结构的主要材料。 应将此参数解释为对 psk3d： Job3DMaterials 属性的已命名子属性的引用。

Job3DSupportsMaterial 关键字配置文件

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
<td>psk3d:Job3DSupportsMaterial</td>
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
<td><p>psk3d： Job3DSupportsMaterial 是一种 QNameParamType，如中的第2.1.3.1 节 " &lt; psf： ParameterDef &gt; " 中所述：</p>
<p><strong>子级：</strong> QNameParamType</p>
<p><strong>描述：</strong></p>
<p>Psf： MinLength 属性值必须是大于或等于1的整数。</p>
<p>Psf： MaxLength 属性值可以由供应商定义，并且必须大于或等于 psf： MinLength 属性值。 它应该是1024。</p>
<p>Psf：必需的属性值必须是 psk： Optional。</p>
<p>Psf： Unittype.pixel 度量属性值必须为个字符。</p></td>
</tr>
</tbody>
</table>



Job3DSupportsMaterial 初始化配置文件

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
<td>psk3d:Job3DSupportsMaterial</td>
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
<p><strong>xsi： type：</strong> Xsd： QName</p>
<p><strong>值：</strong> MaterialName</p>
<p><strong>说明：</strong> MaterialName 必须引用标识为 psk3D： Job3DMaterials 属性子级的材料。</p></td>
</tr>
</tbody>
</table>



Job3DSupportsMaterial 关键字用法

参数定义如下所示：

```cpp
<psf:ParameterDef name="psk3d:Job3DSupportsMaterial">
    <psf:Property name="psf:DataType">
        <psf:Value xsi:type="xsd:QName">xsd:QName</psf:Value>
    </psf:Property>
    <psf:Property name="psf:DefaultValue">
        <psf:Value xsi:type="xsd:QName">vnd:ABS_RED</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MaxLength">
        <psf:Value xsi:type="xsd:integer">1024</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MinLength">
        <psf:Value xsi:type="xsd:integer">1</psf:Value>
    </psf:Property>
    <psf:Property name="psf:Mandatory">
        <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
    </psf:Property>
    <psf:Property name="psf:UnitType">
        <psf:Value xsi:type="xsd:string">characters</psf:Value>
    </psf:Property>
</psf:ParameterDef>
```

此参数的初始化如下：

```cpp
<psf:ParameterInit name="psk3d:Job3DSupportsMaterial">
    <psf:Value xsi:type="xsd:QName">vnd:PLA_TEAL</psf:Value>
</psf:ParameterInit>
```

## <a name="34-job3draft"></a>3.4. Job3DRaft


Psk3d： Job3DRaft 关键字指定此作业是否应包含设备或驱动程序生成的 *筏* 。

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
<td>psk3d:Job3DRaft</td>
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
<p><strong>子级：</strong> 选项 psk3d： RaftIncluded</p>
<p><strong>说明：</strong> 此选项指定设备应为模型生成筏。</p>
<p><strong>子级：</strong> 选项 psk3d： RaftExcluded</p>
<p><strong>说明：</strong> 此选项指定设备不应为模型生成筏。</p></td>
</tr>
</tbody>
</table>



Job3DRaft 关键字用法

```cpp
<psf:Feature name="psk3d:Job3DRaft">
    <psf:Property name="SelectionType">
        <psf:Value xsi:type="xsd:QName">psk:PickOne</psf:Value>
    </psf:Property>
    <psf:Option name="psk3d:RaftIncluded" />
    <psf:Option name="psk3d:RaftExcluded" />
</psf:Feature>
```

### <a name="341-job3draftmaterial"></a>3.4.1. Job3DRaftMaterial

如果选择了选项 psk3d： RaftIncluded，并且设备支持多个材料，则此参数应指示用于筏的主要材料。 应将此参数解释为对 psk3d： Job3DMaterials 属性的已命名子属性的引用。

Job3DRaftMaterial 关键字配置文件

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
<td>psk3d:Job3DRaftMaterial</td>
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
<td><p>psk3d： Job3DRaftMaterial 是一种 QNameParamType，如中的第2.1.3.1 节 " &lt; psf： ParameterDef &gt; " 中所述：</p>
<p><strong>子级：</strong> QNameParamType</p>
<p><strong>描述：</strong></p>
<p>Psf： MinLength 属性值必须是大于或等于1的整数。</p>
<p>Psf： MaxLength 属性值可以由供应商定义，并且必须大于或等于 psf： MinLength 属性值。 它应该是1024。</p>
<p>Psf：必需的属性值必须是 psk： Optional。</p>
<p>Psf： Unittype.pixel 度量属性值必须为个字符。</p></td>
</tr>
</tbody>
</table>



Job3DRaftMaterial 初始化配置文件

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
<td>psk3d:Job3DRaftMaterial</td>
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
<p><strong>xsi： type：</strong> Xsd： QName</p>
<p><strong>值：</strong> MaterialName</p>
<p><strong>说明：</strong> MaterialName 必须引用标识为 psk3D： Job3DMaterials 属性子级的材料。</p></td>
</tr>
</tbody>
</table>



Job3DRaftMaterial 关键字用法

参数定义如下所示：

```cpp
<psf:ParameterDef name="psk3d:Job3DRaftMaterial">
    <psf:Property name="psf:DataType">
        <psf:Value xsi:type="xsd:QName">xsd:QName</psf:Value>
    </psf:Property>
    <psf:Property name="psf:DefaultValue">
        <psf:Value xsi:type="xsd:QName">vnd:ABS_RED</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MaxLength">
        <psf:Value xsi:type="xsd:integer">1024</psf:Value>
    </psf:Property>
    <psf:Property name="psf:MinLength">
        <psf:Value xsi:type="xsd:integer">1</psf:Value>
    </psf:Property>
    <psf:Property name="psf:Mandatory">
        <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
    </psf:Property>
    <psf:Property name="psf:UnitType">
        <psf:Value xsi:type="xsd:string">characters</psf:Value>
    </psf:Property>
</psf:ParameterDef>
```

此参数的初始化如下：

```cpp
<psf:ParameterInit name="psk3d:Job3DRaftMaterial">
    <psf:Value xsi:type="xsd:QName">vnd:PLA_TEAL</psf:Value>
</psf:ParameterInit>
```

## <a name="35-material-mapping-parameter"></a>3.5. 材料映射参数


如果设备支持多个材料，此参数应该指示负载文件中的 basematerials (ID： index) 列表，以映射到特定的输出材料。 Id 必须引用有效负载文件中的 basematerials 元素，因为不允许映射其他类型的材料。 Job3DMaterialSelected) 指定的输出材料 (必须是 psk3d： Job3DMaterials 属性的子元素。 材料映射参数的名称必须以 "Job3D" 开头，并追加 psk3d： Job3DMaterialSelected 属性的值，并在末尾追加 "Map"。 通过这种方式，可以对整个材料地图分析打印票证，而无需打印功能，从而允许将作业移植到其他可能具有相同材料但按不同顺序加载的打印机。

材料映射参数关键字配置文件

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
<td><em>指定的供应商</em></td>
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
<td><p>材料映射参数为 MaterialMapParamType，如本文档的1.8.1 部分中所述。：</p>
<p><strong>子级：</strong> MaterialMapParamType</p>
<p><strong>描述：</strong></p>
<p>Psf： MinLength 属性值必须是大于或等于1的整数。</p>
<p>Psf： MaxLength 属性值可以由供应商定义，并且必须大于或等于 psf： MinLength 属性值。 它应该是1024。</p>
<p>Psf：必需的属性值必须是 psk： Optional。</p>
<p>Psf： Unittype.pixel 度量属性值必须为 materialMapUnitType。</p>
<p>Psk3d： Job3DMaterialSelected 属性值必须引用 Job3DMaterials 属性的子属性的名称。</p></td>
</tr>
</tbody>
</table>



Job3DRaftMaterial 初始化配置文件

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
<td><em>指定的供应商</em></td>
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
<p><strong>xsi： type：</strong> Psk3d:MaterialMapUnitType</p>
<p><strong>值：</strong> 材料列表</p>
<p><strong>说明：</strong> 材料列表必须是以分号分隔的材料 ID：索引值的列表，在模型有效负载中引用 basematerials。</p></td>
</tr>
</tbody>
</table>



材料映射参数关键字用法

参数定义如下所示：

```cpp
   <psf:ParameterDef name="vnd:Job3DABS_REDMap">
       <psf:Property name="psf:DataType">
          <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
       </psf:Property>
       <psf:Property name="psf:MinLength">
          <psf:Value xsi:type="xsd:integer">1</psf:Value>
       </psf:Property>
       <psf:Property name="psf:MaxLength">
          <psf:Value xsi:type="xsd:integer">1024</psf:Value>
       </psf:Property>
       <psf:Property name="psf:Mandatory">
          <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
       </psf:Property>
       <psf:Property name="psf:UnitType">
          <psf:Value xsi:type="xsd:string">characters</psf:Value>
       </psf:Property>
       <psf:Property name="psk3d:Job3DMaterialSelected">
          <psf:Value xsi:type="xsd:QName">vnd:ABS_RED</psf:Value>
       </psf:Property>
   </psf:ParameterDef>
   <psf:ParameterDef name="vnd:Job3DPLA_TEALMap">
       <psf:Property name="psf:DataType">
          <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
       </psf:Property>
       <psf:Property name="psf:MinLength">
          <psf:Value xsi:type="xsd:integer">1</psf:Value>
       </psf:Property>
       <psf:Property name="psf:MaxLength">
          <psf:Value xsi:type="xsd:integer">1024</psf:Value>
       </psf:Property>
       <psf:Property name="psf:Mandatory">
          <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
       </psf:Property>
       <psf:Property name="psf:UnitType">
          <psf:Value xsi:type="xsd:string">characters</psf:Value>
       </psf:Property>
       <psf:Property name="psk3d:Job3DMaterialSelected">
          <psf:Value xsi:type="xsd:QName">vnd:PLA_TEAL</psf:Value>
       </psf:Property>
   </psf:ParameterDef>
```

此参数的初始化如下：

```cpp
   psf:ParameterInit name="vnd:Job3DABS_REDMap">
      <psf:Value xsi:type="xsd:string">1:0;1:2</psf:Value>
   </psf:ParameterInit>
   <psf:ParameterInit name="vnd:Job3DPLA_TEALMap">
      <psf:Value xsi:type="xsd:string">1:1</psf:Value>
   </psf:ParameterInit>
```








