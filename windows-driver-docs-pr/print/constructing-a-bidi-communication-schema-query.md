---
title: 构造 Bidi 通信架构查询
description: 构造 Bidi 通信架构查询
ms.assetid: b18fc69a-652c-4e36-83b3-fc4715b03c0f
keywords:
- 双向通信架构 WDK 打印
- 双向通信架构 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13411cf556ba8ec1e96aeda0a7270aa07e3379b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542189"
---
# <a name="constructing-a-bidi-communication-schema-query"></a>构造 Bidi 通信架构查询


有三个点，在构造 bidi 通信架构查询时要记住：

1.  查询必须开头`Printer`属性，它必须前面加反斜杠字符 (`\`)。

2.  在查询中的任何属性必须分隔句点字符 (`.`)。

3.  如果查询包含一个值，必须用冒号分隔从其父属性值 (`:`)。

### <a href="" id="example-request-and-response"></a> 示例请求和响应

下面的示例所需的 XML 查询和响应格式[bidi 通信接口](https://msdn.microsoft.com/library/windows/hardware/ff545163)，并专门通过 IBidiSpl2 COM 接口。 第一个示例是包含两个架构的请求。 第一个架构确定是否安装了双面打印单元。 第二个架构确定其硬盘相关联的值。

```cpp
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema="\Printer.Configuration.DuplexUnit:Installed"/>
  <Query schema="\Printer.Configuration.HardDisk"/>
</bidi:Get>
```

下一个示例是从第一个示例中的架构的典型响应的一组。 第一个响应指示安装了双面打印单元。 剩余响应指示已安装硬盘，而其容量为 20 MB，其中有 10 MB 是未使用。

```cpp
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema="\Printer.Configuration.DuplexUnit:Installed">
    <Schema name="\Printer.Configuration.DuplexUnit:Installed">
      <BIDI_BOOL>true</BIDI_BOOL>
    </Schema>
  </Query>
  <Query schema="\Printer.Configuration.HardDisk">
    <Schema name="\Printer.Configuration.HardDisk:Installed">
      <BIDI_BOOL>true</BIDI_BOOL>
    </Schema>
    <Schema name="\Printer.Configuration.HardDisk:Capacity">
      <BIDI_INT>20</BIDI_INT>
    </Schema>
    <Schema name="\Printer.Configuration.HardDisk:FreeSpace">
      <BIDI_INT>10</BIDI_INT>
    </Schema>
  </Query>
</bidi:Get>
```

### <a href="" id="additional-query-examples"></a> 其他查询示例

以下是典型的任务和关联的查询的列表：

<a href="" id="determine-whether-a-duplex-unit-is-installed-"></a>确定是否安装了双面打印单元。  
```cpp
\Printer.Configuration.DuplexUnit:Installed
```

<a href="" id="determine-which-input-bins-are-present-"></a>确定哪些输入的箱存在。  
```cpp
\Printer.Layout.InputBins
```

<a href="" id="determine-all-information-about-the-tray1-input-bin-"></a>确定纸盒 1 送纸器有关的所有信息。  
```cpp
\Printer.Layout.InputBins.Tray1
```

<a href="" id="determine-whether-the-tray1-input-bin-is-installed-"></a>确定是否安装了纸盒 1 送的纸盒。  
```cpp
\Printer.Layout.InputBins.Tray1:Installed
```

<a href="" id="determine-the-level-of-black-toner-identified-by--name--blk3e-"></a>确定由黑色墨粉别的\[名称\]Blk3E。  
```cpp
\Printer.Consumables.Blk3E:Level
```

<a href="" id="determine-the-level-of-fuser-oil-"></a>确定杂醇油级别。  
```cpp
\Printer.Consumables.FuserOil:Level
```

 

 




