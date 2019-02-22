---
title: WSD 端口监视器 Bidi 扩展示例
description: WSD 端口监视器 Bidi 扩展示例
ms.assetid: a04f16d5-ae99-4df5-bb55-aef95bd03588
keywords:
- bidi 扩展文件 WDK 打印机自动配置
- 框中自动配置支持 WDK 打印机，bidi 扩展名为的文件
- WSD 架构扩展 WDK 打印机
- 架构扩展 WDK WSD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0738fc4f183ee29829f3b650e41347c04951d757
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521391"
---
# <a name="bidi-extension-example-for-wsd-port-monitor"></a>WSD 端口监视器 Bidi 扩展示例

下面的代码示例是为 Web Services for Devices (WSD) 端口监视器扩展 bidi 通信架构的示例 XML 文件：

```xml
<?xml version='1.0'?>
<bidi:Definition xmlns:bidi='http://schemas.microsoft.com/windows/2005/03/printing/bidi'>

  <Schema xmlns:nprt='http://schemas.microsoft.com/windows/2006/08/wdp/print'>
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

上面的示例 bidi 扩展文件包含的根元素&lt;定义&gt;，与两个主要部分：&lt;架构&gt;，其中放置 bidi 架构扩展，并&lt;PortStatus&gt;、 驱动程序将 WSD 状态映射到端口\_信息\_3 端口 （在 Windows SDK 中所述的状态结构文档）。

架构扩展中使用任何命名空间必须在架构元素中定义。 扩展处理将无法识别较低级别元素中定义的命名空间。 在较低级别元素中定义一个命名空间将导致验证失败的扩展文件。

```xml
<Definition>
  <Schema>...</Schema>
  <PortStatus>...</PortStatus>
</Definition>
```

此扩展插件文件中的每个 bidi 查询包括：

-   描述如何编写 bidi 数据从 WSD; 算法可以使用四个构造定义算法[常量](const.md)，[已安装](installed.md)，[列表](list.md)，以及[值](value.md)。

-   介绍如何获取 WSD 数据 WSD 查询参数。

-   XPath 筛选器的筛选器可用于撰写 bidi 结果的 WSD 架构中的特定 XML 元素。

### <a name="parameter-construct"></a>参数构造

&lt;参数&gt;前面的示例 bidi 扩展文件中使用的元素定义一个变量的属性，可以采用不同值 （例如，TopBin 或 BottomBin），以便可使用以下形式的查询：

-   `\Printer.Layout.InputBins.TopBin:Installed`

-   `\Printer.Layout.InputBins.BottomBin:Installed`

下面的示例查询演示如何使用在前面的 bidi 扩展中定义的自定义属性：

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

前面的示例生成以下查询：

`\Printer.Layout.InputBins.[TrayName]:Installed`
