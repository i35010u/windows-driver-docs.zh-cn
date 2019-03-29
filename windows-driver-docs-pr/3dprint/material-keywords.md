---
title: 材料关键字
description: 这些关键字描述原始材料中用于创建三维对象的设备。
ms.assetid: B2264CA8-64F9-4A20-AC55-46A0C48EDF3C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a105e855aecd5eecd238d2edafde8e9cb25ecb8
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464015"
---
# <a name="material-keywords"></a>材料关键字


这些关键字描述原始材料中用于创建三维对象的设备。

## <a name="31-job3dmaterialcount"></a>3.1. Job3DMaterialCount


此参数必须定义数量的设备，可在单个作业中当前加载的材料。 如果设备不知道在加载材料时，此参数必须是单个作业中使用的材料可能数。 如果打印机具有仅单一、 未知材料，此参数可能会省略，以及所有其他材料关键字。

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
<td>对有效</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>包含 1&lt;值&gt;子元素，按如下所示：</p>
<p><strong>子项：</strong>值</p>
<p><strong>xsi: type:</strong> xsd: integer</p>
<p><strong>值：</strong>JobMaterialCountText</p>
<p><strong>描述:</strong>JobMaterialCountText，如果指定此属性，则必须包含一个正整数，用于标识此设备可用的材料的数目。</p></td>
</tr>
</tbody>
</table>



Job3DMaterialCount 关键字的用法

```cpp
<psf:Property name="psk3d:Job3DMaterialCount">
    <psf:Value xsi:type="xsd:integer">2</psf:Value>
</psf:Property>
```

## <a name="32-job3dmaterials"></a>3.2. Job3DMaterials


此属性必须包含加载到设备中的材料的说明，或如果这是未知的必须包含的材料可加载的可能位置的枚举。

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
<td>对有效</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>包含一个或多个子属性元素，如下所示：</p>
<p><strong>子项：</strong>属性列表</p>
<p><strong>xsi: type:</strong>不可用</p>
<p><strong>值：</strong>MaterialsList</p>
<p><strong>描述:</strong>MaterialsList 包含一组子属性。</p></td>
</tr>
</tbody>
</table>



### <a name="321-materialslist-properties"></a>3.2.1. MaterialsList 属性

供应商必须创建自己的材料，枚举在其设备中加载的打印材料。 这些资料的名称都是供应商定义的并且应表示股票的说明，如果设备能够从加载材料插件读取此类信息。 如果设备不具备此信息，供应商应定义为描述此材料 （例如，"左侧 Extruder"） 的加载位置的材料的名称。

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
<td>psk:DisplayName</td>
<td>xsd:string</td>
<td>此属性应包含 psf:Value 元素包含的本地化的显示名称。</td>
</tr>
<tr class="even">
<td>psk3d:MaterialColor</td>
<td>xsd:string</td>
<td><p>设备可能会定义此属性指定的材料的颜色。 如果指定，值必须是符合下面的说明的 sRGB 颜色：</p>
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
<p>hR、 hG、 hB，和 hA 红色、 绿色、 蓝色和 alpha 组件的十六进制单字节值分别指定，范围从 00 到 FF。 设备可能会忽略 alpha (即 #hRhGhB) 中的事例的 alpha 采用 FF 的默认值 （完全不透明）。</p></td>
</tr>
</tbody>
</table>



Job3DMaterials 关键字的用法

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


Psk3d:Job3DSupports 关键字指定是否应包含此作业*支持*设备或驱动程序生成的。

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
<p><strong>子项：</strong>选项 psk3d:SupportsIncluded</p>
<p><strong>描述:</strong>此选项指定设备应生成模型的外部支持。</p>
<p><strong>子项：</strong>选项 psk3d:SupportsExcluded</p>
<p><strong>描述:</strong>此选项指定在设备不应生成模型的外部支持。</p></td>
</tr>
</tbody>
</table>



Job3DSupports 关键字的用法

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

如果选择选项 psk3d:SupportsIncluded 和设备支持多个材料，此参数应指示要用于支持结构的主材料。 此参数应解释为对已命名子项 psk3d:Job3DMaterials 属性的属性的引用。

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
<td>对有效</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterDef</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>psk3d:Job3DSupportsMaterial 是 QNameParamType §2.1.3.1 中, 所述"&lt;psf:ParameterDef&gt;"打印架构规范中：</p>
<p><strong>子项：</strong>QNameParamType</p>
<p><strong>描述:</strong></p>
<p>Psf:MinLength 属性值必须是大于或等于 1 的整数。</p>
<p>Psf:MaxLength 属性值可能由供应商定义，必须是大于或等于 psf:MinLength 属性值。 它应该是 1024年。</p>
<p>属性值必须 psf:Mandatory 是 psk： 可选。</p>
<p>Psf:UnitType 属性值必须为字符。</p></td>
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
<td>对有效</td>
<td>PrintTicket 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterInit</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>包含 1&lt;值&gt;子元素，按如下所示：</p>
<p><strong>子项：</strong>ReplTest1</p>
<p><strong>xsi: type:</strong> xsd: qname</p>
<p><strong>值：</strong>MaterialName</p>
<p><strong>描述:</strong>MaterialName 必须引用标识为 psk3D:Job3DMaterials 属性子材料。</p></td>
</tr>
</tbody>
</table>



Job3DSupportsMaterial 关键字的用法

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

此参数进行初始化，如下所示：

```cpp
<psf:ParameterInit name="psk3d:Job3DSupportsMaterial">
    <psf:Value xsi:type="xsd:QName">vnd:PLA_TEAL</psf:Value>
</psf:ParameterInit>
```

## <a name="34-job3draft"></a>3.4. Job3DRaft


Psk3d:Job3DRaft 关键字指定是否应包含此作业*筏*设备或驱动程序生成的。

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
<td>“属性”</td>
<td>psk3d:Job3DRaft</td>
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
<p><strong>子项：</strong>Option psk3d:RaftIncluded</p>
<p><strong>描述:</strong>此选项指定设备应生成模型的一系列。</p>
<p><strong>子项：</strong>选项 psk3d:RaftExcluded</p>
<p><strong>描述:</strong>此选项指定在设备不应生成模型的一系列。</p></td>
</tr>
</tbody>
</table>



Job3DRaft 关键字的用法

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

如果选择选项 psk3d:RaftIncluded 和设备支持多个材料，此参数应指示要用于筏的主材料。 此参数应解释为对已命名子项 psk3d:Job3DMaterials 属性的属性的引用。

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
<td>对有效</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterDef</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>psk3d:Job3DRaftMaterial 是 QNameParamType §2.1.3.1 中, 所述"&lt;psf:ParameterDef&gt;"打印架构规范中：</p>
<p><strong>子项：</strong>QNameParamType</p>
<p><strong>描述:</strong></p>
<p>Psf:MinLength 属性值必须是大于或等于 1 的整数。</p>
<p>Psf:MaxLength 属性值可能由供应商定义，必须是大于或等于 psf:MinLength 属性值。 它应该是 1024年。</p>
<p>属性值必须 psf:Mandatory 是 psk： 可选。</p>
<p>Psf:UnitType 属性值必须为字符。</p></td>
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
<td>对有效</td>
<td>PrintTicket 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterInit</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>包含 1&lt;值&gt;子元素，按如下所示：</p>
<p><strong>子项：</strong>ReplTest1</p>
<p><strong>xsi: type:</strong> xsd: qname</p>
<p><strong>值：</strong>MaterialName</p>
<p><strong>描述:</strong>MaterialName 必须引用标识为 psk3D:Job3DMaterials 属性子材料。</p></td>
</tr>
</tbody>
</table>



Job3DRaftMaterial 关键字的用法

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

此参数进行初始化，如下所示：

```cpp
<psf:ParameterInit name="psk3d:Job3DRaftMaterial">
    <psf:Value xsi:type="xsd:QName">vnd:PLA_TEAL</psf:Value>
</psf:ParameterInit>
```

## <a name="35-material-mapping-parameter"></a>3.5. 材料映射参数


如果设备支持多个材料，此参数应指示要将映射到特定输出材料的有效负载文件从 basematerials (ID:index) 的列表。 Id 必须引用有效负载文件中的 basematerials 元素，因为不允许映射其他类型的材料。 （由 Job3DMaterialSelected 指定） 的输出材料必须是 psk3d:Job3DMaterials 属性的子级。 名称材料映射参数必须以"Job3D"开头，并且具有与"映射"追加到末尾追加 psk3d:Job3DMaterialSelected 属性的值。 这样一来，可以为整个材料映射无需打印功能，从而使可移植到其他打印机可能具有相同的材料，但按不同顺序加载作业分析打印票证。

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
<td>对有效</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>ParameterDef</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>材料映射参数 MaterialMapParamType，如中所述的本文档的部分 1.8.1。:</p>
<p><strong>子项：</strong>MaterialMapParamType</p>
<p><strong>描述:</strong></p>
<p>Psf:MinLength 属性值必须是大于或等于 1 的整数。</p>
<p>Psf:MaxLength 属性值可能由供应商定义，必须是大于或等于 psf:MinLength 属性值。 它应该是 1024年。</p>
<p>属性值必须 psf:Mandatory 是 psk： 可选。</p>
<p>属性值必须 psf:UnitType 是 materialMapUnitType。</p>
<p>属性值必须 psk3d:Job3DMaterialSelected 引用的子节点的 Job3DMaterials 属性的名称。</p></td>
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
<td>“属性”</td>
<td><em>指定的供应商</em></td>
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
<p><strong>xsi: type:</strong>Psk3d:MaterialMapUnitType</p>
<p><strong>值：</strong>材料列表</p>
<p><strong>描述:</strong>材料列表必须是以分号分隔的材料 ID:index 值列表引用 basematerials 模型有效负载中。</p></td>
</tr>
</tbody>
</table>



材料映射参数关键字的用法

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

此参数进行初始化，如下所示：

```cpp
   psf:ParameterInit name="vnd:Job3DABS_REDMap">
      <psf:Value xsi:type="xsd:string">1:0;1:2</psf:Value>
   </psf:ParameterInit>
   <psf:ParameterInit name="vnd:Job3DPLA_TEALMap">
      <psf:Value xsi:type="xsd:string">1:1</psf:Value>
   </psf:ParameterInit>
```








