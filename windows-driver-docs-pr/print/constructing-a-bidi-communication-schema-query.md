---
title: 构造双向通信架构查询
description: 构造双向通信架构查询
ms.assetid: b18fc69a-652c-4e36-83b3-fc4715b03c0f
keywords:
- 双向通信架构 WDK 打印
- 双向通信架构 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f14581e557728897d1d7cdfa5e43962271a598df
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652856"
---
# <a name="constructing-a-bidi-communication-schema-query"></a>构造双向通信架构查询


构造双向通信架构查询时，请记住以下三个要点：

1.  查询必须以 `Printer` 属性开始，该属性前面必须有一个反斜杠字符（`\`）。

2.  查询中的所有属性必须用句点字符（`.`）分隔。

3.  如果查询包含一个值，则该值必须通过冒号（`:`）与其父属性隔开。

### <a href="" id="example-request-and-response"></a>示例请求和响应

下面是[双向通信接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)所需的 XML 查询和响应格式的示例，尤其是 IBidiSpl2 COM 接口。 第一个示例是包含两个架构的请求。 第一个架构确定是否安装了双面打印单元。 第二个架构确定与硬盘相关联的值。

```cpp
<bidi:Get xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema="\Printer.Configuration.DuplexUnit:Installed"/>
  <Query schema="\Printer.Configuration.HardDisk"/>
</bidi:Get>
```

下一个示例是第一个示例中的架构的一组典型响应。 第一个响应表明已安装双面打印单元。 剩余的响应表示硬盘已安装，其容量为 20 MB，其中未使用 10 MB。

```cpp
<bidi:Get xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
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

### <a href="" id="additional-query-examples"></a>其他查询示例

下面是典型任务和关联查询的列表：

<a href="" id="determine-whether-a-duplex-unit-is-installed-"></a>确定是否安装了双面打印单元。  
```cpp
\Printer.Configuration.DuplexUnit:Installed
```

<a href="" id="determine-which-input-bins-are-present-"></a>确定存在的输入箱。  
```cpp
\Printer.Layout.InputBins
```

<a href="" id="determine-all-information-about-the-tray1-input-bin-"></a>确定有关 Tray1 输入箱的所有信息。  
```cpp
\Printer.Layout.InputBins.Tray1
```

<a href="" id="determine-whether-the-tray1-input-bin-is-installed-"></a>确定是否安装了 Tray1 输入 bin。  
```cpp
\Printer.Layout.InputBins.Tray1:Installed
```

<a href="" id="determine-the-level-of-black-toner-identified-by--name--blk3e-"></a>确定 \[名称\] Blk3E 标识的黑色碳粉水平。  
```cpp
\Printer.Consumables.Blk3E:Level
```

<a href="" id="determine-the-level-of-fuser-oil-"></a>确定热熔器油的级别。  
```cpp
\Printer.Consumables.FuserOil:Level
```

 

 




