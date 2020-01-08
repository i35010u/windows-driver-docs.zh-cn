---
title: 设备控制关键字
description: 这些关键字用于向3D 制造设备提供控制。
ms.assetid: 1F0CBFC4-F641-4D82-9173-C89218E822B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42941f7056e87d85962a123cccb5692a0baeea84
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652783"
---
# <a name="device-control-keywords"></a>设备控制关键字


这些关键字用于向3D 制造设备提供控制。

## <a name="21-job3doutputarea"></a>2.1. Job3DOutputArea


应使用 psk3d： Job3DOutputArea 属性来定义设备实际打印的区域的大小： Job3DOutputArea 的左下角定义为（0，0，0）。 Job3DOutputAreaWidth、Job3DOutputAreaDepth 和 Job3DOutputAreaHeight 属性定义打印卷的边界框，而如果打印卷不是 cuboid，则 Job3DOutputAreaMesh 可以选择定义该边界框内的确切打印量。

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
<td>psk3d:Job3DOutputArea</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>仅包含1个 &lt;值&gt; 子元素，该元素必须包含 Job3DOutputAreaWidth、Job3DOutputAreaDepth 和 Job3DOutputAreaHeight 属性，并且可能包含 Job3DOutputAreaMesh。</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong>不适用</p>
<p><strong>值：</strong>OutputDimensions</p>
<p><strong>说明：</strong>OutputDimensions 包含构成每个输出区域维度的3个属性集。</p></td>
</tr>
</tbody>
</table>

 

Job3DOutputArea 关键字用法

```xml
<psf:Property name="psk3d:Job3DOutputArea">
    <psf:Property name="psk3d:Job3DOutputAreaWidth">
        <psf:Value xsi:type="xsd:integer">285000</psf:Value>
    </psf:Property>
    <psf:Property name="psk3d:Job3DOutputAreaDepth">
        <psf:Value xsi:type="xsd:integer">153000</psf:Value>
    </psf:Property>
    <psf:Property name="psk3d:Job3DOutputAreaHeight">
        <psf:Value xsi:type="xsd:integer">155000</psf:Value>
    </psf:Property>
     <psf:Property name="psk3d:Job3DOutputAreaMesh">
         <psf:Value xsi:type="xsd:string">
          <![CDATA[
            <mesh xmlns="https://schemas.microsoft.com/3dmanufacturing/mesh/2014/11" unit="millimeter">
             <vertices>
                <vertex x="0" y="0" z="0" />
                <vertex x="0" y="153000" z="0" />
                <vertex x="285000" y="0" z="0" />
                <vertex x="0" y="0" z="155000" />
             </vertices>
             <triangles>
                <triangle v1="0" v2="1" v3="2" />
                <triangle v1="0" v2="2" v3="3" />
                <triangle v1="0" v2="3" v3="1" />
                <triangle v1="2" v2="1" v3="3" />
             </triangles>
          </mesh>
          ]]></psf:Value>
    </psf:Property>
</psf:Property>
```

### <a name="211-job3doutputareawidth"></a>2.1.1. Job3DOutputAreaWidth

描述 microns 中沿 X 轴的输出区域宽度。

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
<td>psk3d:Job3DOutputAreaWidth</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>&gt; 子元素正好包含1个 &lt;值，如下所示：</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong> xsd： integer</p>
<p><strong>值：</strong>OutputWidth</p>
<p><strong>说明：</strong>OutputWidth 必须包含一个大于0的整数，该整数等于 microns 中沿 X 轴的输出区域宽度。</p></td>
</tr>
</tbody>
</table>

 

### <a name="212-job3doutputareadepth"></a>2.1.2. Job3DOutputAreaDepth

描述 microns 中沿 Y 轴方向的输出区域深度。

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
<td>psk3d:Job3DOutputAreaDepth</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>&gt; 子元素正好包含1个 &lt;值，如下所示：</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong> xsd： integer</p>
<p><strong>值：</strong>OutputDepth</p>
<p><strong>说明：</strong>OutputDepth 必须包含一个大于0的整数，该整数等于 microns 中沿 Y 轴的输出区域深度。</p></td>
</tr>
</tbody>
</table>

 

### <a name="213-job3doutputareaheight"></a>2.1.3. Job3DOutputAreaHeight

描述 microns 中沿 Z 轴的输出区域的高度。

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
<td>psk3d:Job3DOutputAreaHeight</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>&gt; 子元素正好包含1个 &lt;值，如下所示：</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong> xsd： integer</p>
<p><strong>值：</strong>OutputHeight</p>
<p><strong>说明：</strong>OutputHeight 必须包含一个大于0的整数，该整数等于沿 Z 轴的输出区域深度，在 microns 中。</p></td>
</tr>
</tbody>
</table>

 

### <a name="214-job3doutputareamesh"></a>2.1.4. Job3DOutputAreaMesh

描述输出卷的形状（如果不是矩形 prism）。 字符串值是一个 XML blob，后面是 &lt;网格&gt; 元素（包含顶点和三角形，并符合3MF 网格的 manifoldness 标准）的3MF 规范。 此多面体必须完全包含在以前的 OutputArea 属性所描述的边界框中。

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
<td>psk3d:Job3DOutputAreaMesh</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>&gt; 子元素正好包含1个 &lt;值，如下所示：</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong> xsd： string</p>
<p><strong>值：</strong>OutputMesh</p>
<p><strong>说明：</strong>OutputMesh 必须包含一个由 "3MF" 规范的 "网格" 部分中定义的顶点和三角形的 xml 字符串，该字符串表示输出卷的边界。</p></td>
</tr>
</tbody>
</table>

 

## <a name="22-job3dappname"></a>2.2. Job3DAppName


设备可以标识默认情况下的工作流应用（此示例包含默认工作流），打印对话框将在选择此打印机时调用。 此工作流应用允许可能需要的任何自定义 UI，或者最好为此设备设置3D 打印作业。

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
<td>psk3d:Job3DAppName</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>&gt; 子元素正好包含1个 &lt;值，如下所示：</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong> xsd： string</p>
<p><strong>值：</strong></p>
<p><strong>说明：</strong>"新式打印" 对话框中用于此打印机的工作流应用的包名称</p></td>
</tr>
</tbody>
</table>

 

Job3DAppName 关键字用法

```xml
<psf:Property name="psk3d:Job3DAppName">
    <psf:Value xsi:type="xsd:string">Microsoft.3DBuilder_8wekyb3d8bbwe</psf:Value>
</psf:Property>
```

## <a name="23-job3dwsdapackagefamilyname"></a>2.3. Job3DWSDAPackageFamilyName


设备可以标识 UWP 设备应用，当用户单击 "**高级设置**" 按钮时，将启动 "打印" 对话框。 此应用提供了用于诸如打印机维护、材料设置、校准等操作的 UI。未提供默认值，因此如果省略此关键字，则不会显示 "**高级设置**" 按钮。

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
<td>psk3d:Job3DWSDAPackageFamilyName</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>&gt; 子元素正好包含1个 &lt;值，如下所示：</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong> xsd： string</p>
<p><strong>值：</strong></p>
<p><strong>说明：</strong>要用于此打印机高级设置的 UWP 设备应用的包名称。</p></td>
</tr>
</tbody>
</table>

 

Job3DWSDAPackageFamilyName 关键字用法

```xml
<psf:Property name="psk3d:Job3DWSDAPackageFamilyName">
    <psf:Value xsi:type="xsd:string"> </psf:Value>
</psf:Property>
```

## <a name="24-job3d3mfversion"></a>2.4. Job3D3MFVersion


设备必须确定要从 Windows 打印系统接收的3MF 文件的版本。 版本由 URI 命名空间从适当版本的核心规范指定。 为了向后兼容，如果省略此关键字，则假定它采用默认值 "<https://schemas.microsoft.com/3dmanufacturing/2013/01”>，这表示不推荐使用的3MF 旧0.93 版本。

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
<td>psk3d:Job3D3MFVersion</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>&gt; 子元素正好包含1个 &lt;值，如下所示：</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong> xsd： string</p>
<p><strong>值：</strong></p>
<p><strong>说明：</strong>定义设备支持的3MF 核心版本作为输入的 URI 命名空间。</p></td>
</tr>
</tbody>
</table>

 

Job3D3MFVersion 关键字用法

```xml
<psf:Property name="psk3d:Job3D3MFVersion">
    <psf:Value xsi:type="xsd:string"> https://schemas.microsoft.com/3dmanufacturing/core/2015/02</psf:Value>
</psf:Property>
```

## <a name="25-job3d3mfextensions"></a>2.5. Job3D3MFExtensions


设备可以指定它理解的3MF 扩展（通过命名空间，形成空格分隔列表），例如允许打印系统发送切片数据（如果有）。

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
<td>psk3d:Job3D3MFExtensions</td>
</tr>
<tr class="even">
<td>适用于</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>内容</td>
<td><p>&gt; 子元素正好包含1个 &lt;值，如下所示：</p>
<p><strong>子级：</strong>负值</p>
<p><strong>xsi： type：</strong> xsd： string</p>
<p><strong>值：</strong></p>
<p><strong>说明：</strong>用空格分隔的 URI 命名空间列表，定义设备支持的3MF 扩展作为输入。</p></td>
</tr>
</tbody>
</table>

 

Job3D3MFExtensions 关键字用法

```xml
<psf:Property name="psk3d:Job3D3MFExtensions">
    <psf:Value xsi:type="xsd:string"> https://schemas.microsoft.com/3dmanufacturing/material/2015/02</psf:Value>
</psf:Property>
```

 

 




