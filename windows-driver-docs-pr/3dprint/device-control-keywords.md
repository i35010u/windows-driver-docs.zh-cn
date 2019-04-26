---
title: 设备控制关键字
description: 这些关键字用于提供对 3D 制造设备的控制。
ms.assetid: 1F0CBFC4-F641-4D82-9173-C89218E822B5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87ec29efb414e47f69866dba34ad695b4763dcb1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325707"
---
# <a name="device-control-keywords"></a>设备控制关键字


这些关键字用于提供对 3D 制造设备的控制。

## <a name="21-job3doutputarea"></a>2.1. Job3DOutputArea


Psk3d:Job3DOutputArea 属性应该用于定义可以实际打印设备的区域的大小： 较低的左下角的 Job3DOutputArea 定义为 (0,0,0)。 Job3DOutputAreaWidth、 Job3DOutputAreaDepth 和 Job3DOutputAreaHeight 属性定义的边界框的打印量，而 Job3DOutputAreaMesh 如果打印量不是 cuboid （可选） 定义该边界框内的确切打印量。

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
<td>对有效</td>
<td>PrintCapabilities 文档</td>
</tr>
<tr class="odd">
<td>元素类型</td>
<td>属性</td>
</tr>
<tr class="even">
<td>目录</td>
<td><p>包含 1&lt;值&gt;子元素，它必须包含 Job3DOutputAreaWidth、 Job3DOutputAreaDepth 和 Job3DOutputAreaHeight 属性，并且可能包含 Job3DOutputAreaMesh。</p>
<p><strong>子项：</strong>值</p>
<p><strong>xsi: type:</strong>不可用</p>
<p><strong>值：</strong>OutputDimensions</p>
<p><strong>描述:</strong>OutputDimensions 包含 3 个构成每个输出区域维度的属性集。</p></td>
</tr>
</tbody>
</table>

 

Job3DOutputArea 关键字的用法

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
            <mesh xmlns="http://schemas.microsoft.com/3dmanufacturing/mesh/2014/11" unit="millimeter">
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

介绍沿 X 轴，微米中输出区域的宽度。

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
<p><strong>值：</strong>OutputWidth</p>
<p><strong>描述:</strong>OutputWidth 必须包含大于 0，它等于微米沿 X 轴，输出区域的宽度的整数。</p></td>
</tr>
</tbody>
</table>

 

### <a name="212-job3doutputareadepth"></a>2.1.2. Job3DOutputAreaDepth

介绍沿 Y 轴，微米中输出区域的深度。

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
<p><strong>值：</strong>OutputDepth</p>
<p><strong>描述:</strong>OutputDepth 必须包含大于 0，它等于微米输出区域沿 Y 轴的深度的整数。</p></td>
</tr>
</tbody>
</table>

 

### <a name="213-job3doutputareaheight"></a>2.1.3. Job3DOutputAreaHeight

介绍沿 Z 轴中微米输出区域的高度。

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
<p><strong>子项：</strong>ReplTest1</p>
<p><strong>xsi: type:</strong> xsd: integer</p>
<p><strong>值：</strong>OutputHeight</p>
<p><strong>描述:</strong>OutputHeight 必须包含大于 0，它等于微米沿 Z 轴中，在输出区域的深度的整数。</p></td>
</tr>
</tbody>
</table>

 

### <a name="214-job3doutputareamesh"></a>2.1.4. Job3DOutputAreaMesh

描述输出量，如果不是矩形 prism 的形状。 字符串值是以下 3MF 规范，用于 XML blob &lt;mesh&gt;元素 （包含顶点和三角形，和有关 3MF 网格符合 manifoldness 标准）。 此多面体必须完全包含在前一 OutputArea 属性所描述的边界框内。

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
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>值：</strong>OutputMesh</p>
<p><strong>描述:</strong>OutputMesh 必须包含顶点和三角形，一个 xml 的字符串的 3MF 规格，它表示输出量的边界的网格部分中定义。</p></td>
</tr>
</tbody>
</table>

 

## <a name="22-job3dappname"></a>2.2. Job3DAppName


设备可能会标识而不是默认 （此示例包含的默认工作流） 的工作流应用程序时选择此打印机，将调用打印对话框。 此工作流应用程序允许可能是必要的或所需 3D 打印作业的最佳设置此设备的任何自定义 UI。

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
<p><strong>子项：</strong>ReplTest1</p>
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>值：</strong></p>
<p><strong>描述:</strong>要用于此打印机现代打印对话框中的工作流应用的包名称</p></td>
</tr>
</tbody>
</table>

 

Job3DAppName 关键字的用法

```xml
<psf:Property name="psk3d:Job3DAppName">
    <psf:Value xsi:type="xsd:string">Microsoft.3DBuilder_8wekyb3d8bbwe</psf:Value>
</psf:Property>
```

## <a name="23-job3dwsdapackagefamilyname"></a>2.3. Job3DWSDAPackageFamilyName


设备可能会标识 UWP 设备应用，打印对话框将启动时**高级设置**用户单击按钮。 此应用显示为诸如打印机维护、 材料的安装程序、 校准等操作显示 UI。提供无默认值，因此，如果省略了此关键字，没有**高级设置**将显示按钮。

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
<p><strong>子项：</strong>ReplTest1</p>
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>值：</strong></p>
<p><strong>描述:</strong>要用于此打印机的 UWP 设备应用包名称的高级设置。</p></td>
</tr>
</tbody>
</table>

 

Job3DWSDAPackageFamilyName 关键字的用法

```xml
<psf:Property name="psk3d:Job3DWSDAPackageFamilyName">
    <psf:Value xsi:type="xsd:string"> </psf:Value>
</psf:Property>
```

## <a name="24-job3d3mfversion"></a>2.4. Job3D3MFVersion


设备必须标识它期望收到从 Windows 打印系统 3MF 文件的版本。 由 URI 命名空间从适当版本的核心规范指定的版本。 有关向后兼容性，如果省略了此关键字，它将假定采用默认值为"<http://schemas.microsoft.com/3dmanufacturing/2013/01”>，指示 0.93 旧版 3MF，不建议这样做。

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
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>值：</strong></p>
<p><strong>描述:</strong>定义 3MF core 版本作为输入设备支持的 URI 命名空间。</p></td>
</tr>
</tbody>
</table>

 

Job3D3MFVersion 关键字的用法

```xml
<psf:Property name="psk3d:Job3D3MFVersion">
    <psf:Value xsi:type="xsd:string"> http://schemas.microsoft.com/3dmanufacturing/core/2015/02</psf:Value>
</psf:Property>
```

## <a name="25-job3d3mfextensions"></a>2.5. Job3D3MFExtensions


设备可能会 （按命名空间，构成的用空格分隔的列表） 指定 3MF 扩展它能够理解的例如允许打印系统根据可用发送切片数据。

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
<p><strong>子项：</strong>ReplTest1</p>
<p><strong>xsi: type:</strong> xsd: string</p>
<p><strong>值：</strong></p>
<p><strong>描述:</strong>以空格分隔的 URI 命名空间定义支持的作为输入设备 3MF 扩展插件的列表。</p></td>
</tr>
</tbody>
</table>

 

Job3D3MFExtensions 关键字的用法

```xml
<psf:Property name="psk3d:Job3D3MFExtensions">
    <psf:Value xsi:type="xsd:string"> http://schemas.microsoft.com/3dmanufacturing/material/2015/02</psf:Value>
</psf:Property>
```

 

 




