---
title: WSD 端口监视器的双向扩展示例
description: WSD 端口监视器的双向扩展示例
keywords:
- 双向扩展文件 WDK 打印机自动配置
- 内置自动配置支持 WDK 打印机，双向扩展文件
- WSD 架构扩展 WDK 打印机
- 架构扩展 WDK WSD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fde07e778b952dcd721d224596c319ddc7c660f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797819"
---
# <a name="bidi-extension-example-for-wsd-port-monitor"></a>WSD 端口监视器的双向扩展示例

下面的代码示例是一个示例 XML 文件，它为设备 (WSD) 端口监视器扩展了 Web 服务的双向通信架构：

```xml
<?xml version='1.0'?>
<bidi:Definition xmlns:bidi='https://schemas.microsoft.com/windows/2005/03/printing/bidi'>

  <Schema xmlns:nprt='https://schemas.microsoft.com/windows/2006/08/wdp/print'>
    <Property name='Printer'>
      <Property name='DeviceInfo'>
        <Value name='FriendlyName' query='nprt:PrinterDescription' filter='nprt:PrinterDescription/nprt:PrinterName' type='BIDI_STRING' xmllang='true'/>
        <Value name='Location' query='nprt:PrinterDescription' filter='nprt:PrinterDescription/nprt:PrinterLocation' type='BIDI_STRING' xmllang='true'/>
        <Value name='Comment' query='nprt:PrinterDescription' filter='nprt:PrinterDescription/nprt:PrinterInfo' type='BIDI_STRING' xmllang='true'/>
        <Value name='IEEE1284DeviceId' query='nprt:PrinterDescription' filter='nprt:PrinterDescription/nprt:DeviceId' type='BIDI_STRING'/>
      </Property>
      <Property name='Configuration'>
        <Property name='Memory'>
          <Value name='Size' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="RAM"]/nprt:Size' type='BIDI_INT' drvPrinterEvent='true'/>
          <Value name='PS' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="PSMemory"]/nprt:Size' type='BIDI_INT' drvPrinterEvent='true'/>
        </Property>
        <Property name='HardDisk'>
          <Installed name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="HardDisk"]' drvPrinterEvent='true'/>
          <Value name='Capacity' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="HardDisk"]/nprt:Size' type='BIDI_INT' drvPrinterEvent='true'/>
          <Value name='FreeSpace' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Storage/nprt:StorageEntry[nprt:Type="HardDisk"]/nprt:Free' type='BIDI_INT' drvPrinterEvent='true'/>
        </Property>
        <Property name='DuplexUnit'>
          <Value name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:DuplexerInstalled' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
        </Property>
      </Property>
      <Property name='Consumables'>
        <Parameter name='$Name$' parameter='Name' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry/@nprt:Name'>
          <Installed name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]' drvPrinterEvent='true'/>
          <Value name='Type' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]/nprt:Type' type='BIDI_STRING' drvPrinterEvent='true'/>
          <Value name='Color' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]/nprt:Color' type='BIDI_STRING' drvPrinterEvent='true'/>
          <Value name='Level' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]/nprt:Level' type='BIDI_INT' drvPrinterEvent='true'/>
          <Value name='Model' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Consumables/nprt:ConsumableEntry[@nprt:Name="$Name$"]/nprt:Model' type='BIDI_STRING' drvPrinterEvent='true'/>
        </Parameter>
      </Property>
      <Property name='Layout'>
        <Property name='NumberUp'>
          <Property name='PagesPerSheet'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:DocumentProcessing/nprt:NumberUp/nprt:PagesPerSheet' type='BIDI_INT' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:DocumentProcessing/nprt:NumberUp/nprt:PagesPerSheet/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
          <Property name='Direction'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:DocumentProcessing/nprt:NumberUp/nprt:Direction' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:DocumentProcessing/nprt:NumberUp/nprt:Direction/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
        </Property>
        <Property name='Orientation'>
          <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:DocumentProcessing/nprt:Orientation' type='BIDI_STRING' drvPrinterEvent='true'/>
          <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:DocumentProcessing/nprt:Orientation/nprt:AllowedValue' drvPrinterEvent='true'/>
        </Property>
        <Property name='InputBins'>
          <Parameter name='$TrayName$' parameter='TrayName' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry/@nprt:Name'>
            <Installed name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]' drvPrinterEvent='true'/>
            <Value name='MediaSize' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:MediaSize' type='BIDI_STRING' drvPrinterEvent='true'/>
            <Value name='MediaType' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:MediaType' type='BIDI_STRING' drvPrinterEvent='true'/>
            <Value name='MediaColor' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:MediaColor' type='BIDI_STRING' drvPrinterEvent='true'/>
            <Value name='FeedDirection' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:FeedDirection' type='BIDI_STRING' drvPrinterEvent='true'/>
            <Value name='Capacity' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:Capacity' type='BIDI_INT' drvPrinterEvent='true'/>
            <Value name='Level' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:InputBins/nprt:InputBinEntry[@nprt:Name="$TrayName$"]/nprt:Level' type='BIDI_INT' drvPrinterEvent='true'/>
          </Parameter>
        </Property>
      </Property>
      <Property name='Finishing'>
        <Value name='CollationSupported' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:CollationSupported' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
        <Value name='JogOffsetSupported' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:JogOffsetSupported' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
        <Property name='Staple'>
          <Value name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:StaplerInstalled' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
          <Property name='Location'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:JobProcessing/nprt:JobFinishings/nprt:Staple/nprt:Location' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:JobProcessing/nprt:JobFinishings/nprt:Staple/nprt:Location/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
          <Property name='Angle'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:JobProcessing/nprt:JobFinishings/nprt:Staple/nprt:Angle' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:JobProcessing/nprt:JobFinishings/nprt:Staple/nprt:Angle/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
        </Property>
        <Property name='HolePunch'>
          <Value name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:Finishings/nprt:HolePunch/nprt:HolePunchInstalled' type='BIDI_BOOL' optional='true' drvPrinterEvent='true'>false</Value>
          <Property name='Pattern'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:JobProcessing/nprt:JobFinishings/nprt:HolePunch/nprt:Pattern' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:JobProcessing/nprt:JobFinishings/nprt:HolePunch/nprt:Pattern/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
          <Property name='Location'>
            <Value name='CurrentValue' query='nprt:DefaultPrintTicket' filter='nprt:DefaultPrintTicket/nprt:JobProcessing/nprt:JobFinishings/nprt:HolePunch/nprt:Edge' type='BIDI_STRING' drvPrinterEvent='true'/>
            <List name='Supported' query='nprt:PrinterCapabilities' filter='nprt:PrinterCapabilities/nprt:JobValues/nprt:JobProcessing/nprt:JobFinishings/nprt:HolePunch/nprt:Edge/nprt:AllowedValue' drvPrinterEvent='true'/>
          </Property>
        </Property>
        <Property name='OutputBins'>
          <Parameter name='$TrayName$' parameter='TrayName' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:OutputBins/nprt:OutputBinEntry/@nprt:Name'>
            <Installed name='Installed' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:OutputBins/nprt:OutputBinEntry[@nprt:Name="$TrayName$"]' drvPrinterEvent='true'/>
            <Value name='Capacity' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:OutputBins/nprt:OutputBinEntry[@nprt:Name="$TrayName$"]/nprt:Capacity' type='BIDI_INT' drvPrinterEvent='true'/>
            <Value name='Level' query='nprt:PrinterConfiguration' filter='nprt:PrinterConfiguration/nprt:OutputBins/nprt:OutputBinEntry[@nprt:Name="$TrayName$"]/nprt:Level' type='BIDI_INT' drvPrinterEvent='true'/>
          </Parameter>
        </Property>
      </Property>
      <Property name='Status'>
        <Property name='Summary'>
          <Value name='State' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:PrinterState' type='BIDI_STRING'/>
          <Value name='StateReason' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:PrinterPrimaryStateReason' type='BIDI_STRING'/>
        </Property>
        <Property name='Detailed'>
          <Parameter name='Event$EventIndex$' parameter='EventIndex' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition/@nprt:Id'>
            <Value name='Name' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition[@nprt:Id="$EventIndex$"]/nprt:Name' type='BIDI_STRING'/>
            <Value name='Severity' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition[@nprt:Id="$EventIndex$"]/nprt:Severity' type='BIDI_STRING'/>
            <Property name='Component'>
              <Value name='Group' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition[@nprt:Id="$EventIndex$"]/nprt:Component/nprt:Group' type='BIDI_STRING'/>
              <Value name='Name' query='nprt:PrinterStatus' filter='nprt:PrinterStatus/nprt:ActiveCondition/nprt:DeviceCondition[@nprt:Id="$EventIndex$"]/nprt:Component/nprt:Name' type='BIDI_STRING'/>
            </Property>
          </Parameter>
        </Property>
      </Property>
    </Property>
  </Schema>
  <PortStatus>
    <Status>
      <Keyword>None</Keyword>
      <Code>0</Code>
      <Severity>0</Severity>
    </Status>
    <Status>
      <Keyword>AttentionRequired</Keyword>
      <Code>8</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>DoorOpen</Keyword>
      <Code>7</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MarkerFailure</Keyword>
      <ResourceIdOffset>0</ResourceIdOffset>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MarkerSupplyLow</Keyword>
      <Code>10</Code>
      <Severity>2</Severity>
    </Status>
    <Status>
      <Keyword>MarkerSupplyEmpty</Keyword>
      <Code>6</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MediaEmpty</Keyword>
      <Code>3</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MediaJam</Keyword>
      <Code>2</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>MediaLow</Keyword>
      <ResourceIdOffset>1</ResourceIdOffset>
      <Severity>2</Severity>
    </Status>
    <Status>
      <Keyword>MediaNeeded</Keyword>
      <Code>5</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>OutputAreaAlmostFull</Keyword>
      <ResourceIdOffset>2</ResourceIdOffset>
      <Severity>2</Severity>
    </Status>
    <Status>
      <Keyword>OutputAreaFull</Keyword>
      <Code>4</Code>
      <Severity>1</Severity>
    </Status>
    <Status>
      <Keyword>Paused</Keyword>
      <ResourceIdOffset>3</ResourceIdOffset>
      <Severity>3</Severity>
    </Status>
  </PortStatus>
</bidi:Definition>
```

### <a name="description-of-schema-extension"></a>架构扩展的说明

前面的示例双向扩展文件包含根元素 &lt; 定义，其中包含 &gt; 两个主要部分： &lt; 架构 &gt; ，其中包含双向架构扩展， &lt; PortStatus &gt; ，其中，驱动程序将 WSD 状态映射到端口 \_ 信息 \_ 3 端口状态 (结构，如 Windows SDK 文档) 中所述。

架构扩展中使用的所有命名空间都必须在 Schema 元素中定义。 扩展处理将不会识别在较低级别元素中定义的命名空间。 在较低级别元素中定义命名空间会导致扩展文件验证失败。

```xml
<Definition>
  <Schema>...</Schema>
  <PortStatus>...</PortStatus>
</Definition>
```

此扩展文件中的每个双向查询包括：

-   描述如何从 WSD 数据撰写双向数据的算法;可以用四个构造 [常量](const.md)、 [已安装](installed.md)、 [列表](list.md)和 [值](value.md)来定义算法。

-   用于描述如何获取 WSD 数据的 WSD 查询参数。

-   XPath 筛选器，用于筛选要用于撰写双向结果的 WSD 架构中的特定 XML 元素。

### <a name="parameter-construct"></a>参数构造

&lt; &gt; 前面的示例双向扩展文件中使用的 Parameter 元素定义了一个变量属性，该属性可以采用不同的值 (例如，TopBin 或 BottomBin) ，这样就可以使用以下形式的查询：

-   `\Printer.Layout.InputBins.TopBin:Installed`

-   `\Printer.Layout.InputBins.BottomBin:Installed`

下面的示例查询演示如何使用在前面的双向扩展中定义的自定义属性：

```xml
<Property name='Printer'>
  <Property name='Layout'>
    <Property name='InputBins'>
      <Parameter name='$TrayName$'
        parameter='TrayName'
        query='wprt:PrinterConfiguration'
        filter='wprt:PrinterConfiguration/wprt:InputBins/wprt:InputBinEntry/wprt:Name'>
        <Installed
          name='Installed'
          query='wprt:PrinterConfiguration'
          filter='wprt:PrinterConfiguration/wprt:InputBins/wprt:InputBinEntry[wprt:Name="$TrayName$"]'/>
      </Parameter>
    </Property>
  </Property>
</Property>
```

前面的示例将生成以下查询：

`\Printer.Layout.InputBins.[TrayName]:Installed`
