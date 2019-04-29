---
title: TCP/IP 端口监视器的双向扩展示例
description: TCP/IP 端口监视器的双向扩展示例
ms.assetid: 76454b0c-0e02-4372-97ed-2401a785cef8
keywords:
- bidi 扩展文件 WDK 打印机自动配置
- 框中自动配置支持 WDK 打印机，bidi 扩展名为的文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dbcadbc5803c82c622f728ebbf3e390b8c602b3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379265"
---
# <a name="bidi-extension-sample-for-tcpip-port-monitor"></a>TCP/IP 端口监视器的双向扩展示例


下面的代码示例是为标准 TCP/IP 端口监视器扩展 bidi 通信架构的示例 XML 文件。

```xml
<?xml version="1.0" encoding="US-ASCII"?>
<bidi:Schema xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
    <Property name="Printer">
      <Property name="Layout">
        <Property name="InputBins">
          <InputBin name="TopBin"    mibName="TRAY 1"/>
          <InputBin name="BottomBin" mibName="TRAY 2"/>
        </Property>
      </Property>
      <Property name="Finishing">
        <Property name="OutputBins">
          <OutputBin name="TopBin" mibName="Standard Bin"/>
        </Property>
      </Property>
      <Property name="Extension">
        <Property name="Version">
          <Const name="Major" type="BIDI_INT" value="1"/>
          <Const name="Minor" type="BIDI_INT" value="0"/>
        </Property>
        <Property name="System">
          <Value name="Name" type="BIDI_TEXT" oid="1.3.6.1.2.1.1.5"/>
        </Property>
        <Property name="DuplexUnit">
          <Installed name="Installed" oid="1.3.6.1.2.1.43.13.4.1.9"
                     deviceIndex="true">
            <Lookup value="3"/>
            <Lookup value="4"/>
          </Installed>
        </Property>
        <Property name="Channels">
          <Const name="Category" type="BIDI_STRING" value="Channels"/>
          <IndexedProperty name="Channel">
            <Value name="Type" oid="1.3.6.1.2.1.43.14.1.1.2" 
                   type="BIDI_STRING" deviceIndex="true"/>
          </IndexedProperty>
        </Property>
      </Property>
    </Property>
</bidi:Schema>
```

上面的代码示例会导致以下查询：

```cpp
\Printer.Layout.InputBins.TopBin:Installed
\Printer.Layout.InputBins.TopBin:Level
\Printer.Layout.InputBins.TopBin:MediaSize
\Printer.Layout.InputBins.TopBin:MediaType
\Printer.Layout.InputBins.BottomBin:Installed
\Printer.Layout.InputBins.BottomBin:Level
\Printer.Layout.InputBins.BottomBin:MediaSize
\Printer.Layout.InputBins.BottomBin:MediaType
\Printer.Finishing.OutputBins.TopBin:Installed
\Printer.Finishing.OutputBins.TopBin:Level
\Printer.Extension.Version:Major
\Printer.Extension.Version:Minor
\Printer.Extension.System:Name
\Printer.Extension.DuplexUnit:Installed
\Printer.Extension.Channels:Category
\Printer.Extension.Channels.Channel001:Type
```
