---
title: 用于打印的基于设备的 Web 服务 (WS-Print)
description: 设备上用于打印 (WS 打印) 的 Web 服务在 Windows Vista 中引入，以提供用于打印和扫描外围设备的连接协议。
ms.assetid: 4A641EF8-FBD3-46CA-9284-28AF1A4B8226
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cf2cf448e3dbcf8c164b73899445908e0b8a5dc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205871"
---
# <a name="web-services-on-devices-for-printing-ws-print"></a>用于打印的基于设备的 Web 服务 (WS-Print)

设备上用于打印 (WS 打印) 的 Web 服务在 Windows Vista 中引入，以提供用于打印和扫描外围设备的连接协议。

## <a name="overview"></a>概述

Web 服务技术为描述和共享信息提供了通用框架。 因此，Windows 附带了一组用于在网络连接设备上使用和控制服务的协议。

对于打印和扫描存在四个 Web 服务规范，以帮助设备制造商利用改进的客户体验来连接、安装和使用 Windows 设备。

## <a name="ws-print-v11"></a>WS 打印1.1 版

对于 Windows 8， (WSD) 设备上的 web 服务的打印架构已更新到1.1 版。 此版本的架构 (称为 WS 打印1.1 版) 已更新，以支持增强的驱动程序配置、更好的墨迹/墨粉颜色表示形式和设备型号 Id。

## <a name="ws-print-v12"></a>WS 打印版本1。2

对于 Windows 8.1，WS 打印包含 WS 打印1.1 版中使用的所有操作和架构元素，但已更新设备上 web 服务的打印服务定义。 并且生成的用于打印的新 Web 服务为 WS 打印版。

在 WS Print v1.0 中，支持新架构元素，并已添加新操作。 新架构元素 "SupportsWSPrintV12" 用于识别 WS 打印版本1.2 的支持。 新操作 "SetPrinterElements" 使客户端能够在打印机上设置架构元素的值。 例如，客户端可以设置一个名为 "InkHeadAlignmentValue" 的自定义元素，打印机将使用该元素重新调整喷墨打印头。

为方便起见，此处提供了 "下载" 部分的规范，其中包含完整的独立表单，以及与之关联的 Web Services 描述语言 (WSDLs) 和 XML 架构定义 (Xsd) 。 这四个基于设备的 Web 服务规范包含在 (WDK) 的 Windows 驱动程序开发工具包中。

以下各节提供有关 WS 打印的各个方面的更多详细信息。

## <a name="sequence-diagrams"></a>序列图

下面的序列图演示了客户端和打印机之间的交互，以确定支持的 WS 打印命名空间的版本，然后检索扩展的架构元素。

### <a name="ws-print-v11-sequence-diagram"></a>WS 打印 v1.1 序列图

下面是支持 WS 打印版本的打印机的交互序列图：

![显示有关 ws 打印 v1.1 支持的客户端打印机交互，以及用于打印机说明和配置的后续查询的序列图。](images/wsprint-diagv11.png)

如果打印机支持 WS 打印1.1 版，则在响应 GetPrinterElements (wprt： PrinterDescription 从客户端) 查询时，打印机将发送回信息以指示它的作用。

在打印机确认它支持 WS Print v1.1 之后，客户端将发送 GetPrinterElements (wprt11： DriverConfiguration) 查询，打印机将使用请求的驱动程序配置信息进行响应。

### <a name="ws-print-v12-sequence-diagram"></a>WS 打印 v2.0 序列图

下面是支持 WS 打印的打印机的交互序列图：

![显示有关 ws 打印 v1.0 支持的客户端打印机交互，以及用于打印机说明和配置的后续查询的序列图。](images/wsprint-diagv12.png)

如果打印机支持 WS 打印版本1.2，则在响应 GetPrinterElements (wprt： PrinterDescription 从客户端) 查询时，打印机将发送回信息以指示它的功能。

此外，打印机应返回 wprt12： SupportsWSPrintV12 以响应 GetPrinterElements (wprt： PrinterDescription) 调用。 之后，客户端可以调用 SetPrinterElements 操作来设置 WS 打印设备支持的架构中的一个或多个数据元素。

在打印机确认它支持 WS 打印版本1.2 之后，客户端将发送 GetPrinterElements (wprt12： DriverConfiguration) 查询，打印机将使用请求的驱动程序配置信息进行响应。

## <a name="namespaces"></a>命名空间

### <a name="ws-print-v11-namespace"></a>WS 打印 v1.1 命名空间

**命名空间：** `<https://schemas.microsoft.com/windows/2010/06/wdp/printv11>` 
**XML 命名空间定义：**`xmlns:wprt12="<https://schemas.microsoft.com/windows/2012/10/wdp/printV12>"`

### <a name="ws-print-v12-namespace"></a>WS 打印 v1.0 命名空间

**命名空间：** `<https://schemas.microsoft.com/windows/2012/10/wdp/printV12>` 
**XML 命名空间定义：**`xmlns:wprt11="<https://schemas.microsoft.com/windows/2010/06/wdp/printv11>"`

## <a name="specifying-ws-print-11-support"></a>指定 WS 打印1.1 支持

支持 WS 打印1.1 元素的打印机必须将其 PrinterDescription 更新为包含 wprt11： SupportsWSPrintv11。 如果未指定 wprt11： SupportsWSPrintv11 并将其设置为 true，则 WSDMon 不会从打印机请求任何 WS 打印1.1 元素。

支持 WS Print v1.1 的打印设备必须在其 PrinterDescription 中包含以下内容，Windows 才能查询该命名空间中的任何其他元素。

```xml
<soap:Envelope
...
  xmlns:wprt11="https://schemas.microsoft.com/windows/2010/06/wdp/printv11">"
...
  <wprt11:SupportsWSPrintv11>true</wprt11:SupportsWSPrintv11>
...
```

以下 XML 代码段派生自 WSD 打印服务规范 v1.0，它显示了上一节中内容的正确用法。

```xml
<soap:Envelope
        xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
        xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
        xmlns:wprt="https://schemas.microsoft.com/windows/2006/08/wdp/print"
        xmlns:wprt11="https://schemas.microsoft.com/windows/2010/06/wdp/printv11">"
  <soap:Header>
    <wsa:To>https://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      https://schemas.microsoft.com/windows/2006/08/wdp/print/GetPrinterElementsResponse
    </wsa:Action>
    <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
    <wsa:RelatesTo>uuid:MsgIdOfTheGetPrinterElementsRequest</wsa:RelatesTo>
  </soap:Header>
  <soap:Body>
    <wprt:GetPrinterElementsResponse>
      <wprt:PrinterElements>
        <wprt:ElementData Name="wprt:PrinterDescription" Valid="true">
          <wprt:PrinterDescription>
            <wprt:ColorSupported>true</wprt:ColorSupported>
            <wprt:DeviceId>MFG:Acme;MDL:PrintMaster 9020</wprt:DeviceId>
            <wprt:MultipleDocumentJobsSupported>true</wprt:MultipleDocumentJobsSupported>
            <wprt:PagesPerMinute>20</wprt:PagesPerMinute>
            <wprt:PagesPerMinuteColor>8</wprt:PagesPerMinuteColor>
            <wprt:PrinterName xml:lang="en-AU, en-CA, en-GB, en-US">
              Accounting Printer in Copy Room 2
            </wprt:PrinterName>
            <wprt:PrinterInfo xml:lang="en-AU, en-CA, en-GB, en-US">
              Printer for use of Accounting only
            </wprt:PrinterInfo>
            <wprt:PrinterLocation xml:lang="en-AU, en-CA, en-GB, en-US">
              LA Campus – Building 3
            </wprt:PrinterLocation>
            <wprt11:SupportsWSPrintv11>true</wprt11:SupportsWSPrintv11>
          </wprt:PrinterDescription>
        </wprt:ElementData>
      </wprt:PrinterElements>
    </wprt:GetPrinterElementsResponse>
  </soap:Body>
</soap:Envelope>
```

以下 XML 代码片段显示了支持 WS 打印 v1.1 的打印设备的架构。

```xml
<xs:schema targetNamespace="https://schemas.microsoft.com/windows/2010/06/wdp/printv11"
           xmlns:wprt11="https://schemas.microsoft.com/windows/2010/06/wdp/printv11"
           xmlns:xs="https://www.w3.org/2001/XMLSchema"
           elementFormDefault="qualified">

<xs:annotation>
    <xs:documentation>
        WS-Print Extensions for Driver Configuration and Consumable Definition
        Copyright 2010 Microsoft Corp. All rights reserved
    </xs:documentation>
</xs:annotation>

<xs:annotation>
    <xs:documentation> A Boolean element that denotes support for WS-Print V11 extensions
    </xs:documentation>
</xs:annotation>

<xs:element name="SupportsWSPrintv11" type="xs:boolean"/>
```

## <a name="specifying-ws-print-12-support"></a>指定 WS 打印1.2 支持

支持 WS 打印1.2 元素的打印机必须将其 PrinterDescription 更新为包含 wprtV12： SupportsWSPrintV12。 如果未指定 wprtV12： SupportsWSPrintV12 并将其设置为 true，则 WSDMon 不会从打印机请求任何 WS 打印1.2 元素。

支持 WS 打印版1.2 的打印设备必须在其 PrinterDescription 中包含以下内容，Windows 才能查询该命名空间中的任何其他元素。

```xml
<soap:Envelope
…
    xmlns:wprtV12="https://schemas.microsoft.com/windows/2012/10/wdp/printV12">
…
    <wprtV12:SupportsWSPrintV12>true</wprtV12:SupportsWSPrintV12>
…
</soap:Envelope>
```

以下 XML 代码段派生自 WSD 打印服务规范版本1.2，并显示了上一节中内容的正确用法。

```xml
<soap:Envelope
     xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
     xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
     xmlns:wprt="https://schemas.microsoft.com/windows/2006/08/wdp/print"
     xmlns:wprtV12="https://schemas.microsoft.com/windows/2012/10/wdp/printV12">
     <soap:Header>
          <wsa:To>https://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
          <wsa:Action>
               https://schemas.microsoft.com/windows/2006/08/wdp/print/GetPrinterElementsResponse
          </wsa:Action>
          <wsa:MessageID>uuid:UniqueMsgId</wsa:MessageID>
          <wsa:RelatesTo>uuid:MsgIdOfTheGetPrinterElementsRequest</wsa:RelatesTo>
     </soap:Header>
     <soap:Body>
         <wprt:GetPrinterElementsResponse>
            <wprt:PrinterElements>
             <wprt:ElementData Name="wprt:PrinterDescription" Valid="true">
                <wprt:PrinterDescription>
                     <wprt:ColorSupported>true</wprt:ColorSupported>
                         <wprt:DeviceId>MFG:Acme;MDL:PrintMaster 9020</wprt:DeviceId>
                         <wprt:MultipleDocumentJobsSupported>true</wprt:MultipleDocumentJobsSupported>
                     <wprt:PagesPerMinute>20</wprt:PagesPerMinute>
                     <wprt:PagesPerMinuteColor>8</wprt:PagesPerMinuteColor>
                     <wprt:PrinterName xml:lang="en-AU, en-CA, en-GB, en-US">
                             Accounting Printer in Copy Room 2</wprt:PrinterName>
                         <wprt:PrinterInfo xml:lang="en-AU, en-CA, en-GB, en-US">
                             Printer for use of Accounting only</wprt:PrinterInfo>
                         <wprt:PrinterLocation xml:lang="en-AU, en-CA, en-GB, en-US">
                             LA Campus – Building 3</wprt:PrinterLocation>
                         <wprtV12:SupportsWSPrintV12>true</wprtV12:SupportsWSPrintV12>
                    </wprt:PrinterDescription>
             </wprt:ElementData>
            </wprt:PrinterElements>
         </wprt:GetPrinterElementsResponse>
      </soap:Body>
</soap:Envelope>
```

以下三个部分中的架构示例说明了如何使用 WS Print v1.1 引入的一些新元素。 有关随 WS Print v1.1 命名空间引入的所有元素的详细信息，请参阅下面 " **下载** " 部分中列出的 "ws 打印" 的支持文件。

## <a name="enhanced-driver-configuration"></a>增强的驱动程序配置

此架构为此设备提供特定于设备的 GPD 或 PPD 配置文件。

```xml
   <xs:annotation>
        <xs:documentation>Driver Configuration File definition</xs:documentation>
    </xs:annotation>
    <xs:element name="DriverConfiguration" type="wprt11:DriverConfigurationType"/>
    <xs:complexType name="DriverConfigurationType">
        <xs:sequence>
            <xs:element name="GPDConfigFile" type="xs:string" minOccurs="0" />
            <xs:element name="PPDConfigFile" type="xs:string" minOccurs="0" />
            <xs:any namespace="##other" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:anyAttribute namespace="##other" processContents="lax" />
    </xs:complexType>
```

## <a name="device-model-id"></a>设备型号 ID

以下架构描述了设备的 ModelID，用于设备元数据检索。 有关 ModelIDs 的详细信息，请参阅 [ModelID 元素](/previous-versions/windows/hardware/metadata/ff549295(v=vs.85))。

```xml
    <xs:annotation>
        <xs:documentation> Print Device Model Id value for device differentiation</xs:documentation>
        <xs:documentation> Always represented as a GUID</xs:documentation>
    </xs:annotation>
    <xs:element name="DeviceModelId" type="wprt11:DeviceModelIdGuidType"/>
    <xs:simpleType name="DeviceModelIdGuidType">
        <xs:restriction base="xs:string">
            <xs:length value="36"/>
        </xs:restriction>
    </xs:simpleType>
```

## <a name="inktoner-color-representation-value"></a>墨迹/墨粉颜色表示值

以下架构检索表示特定墨迹或碳粉类型的颜色的 RGB 三个。 应为任何墨盒或碳粉补充指定此值，以便能够更好地表示应用 UI 中显示的颜色。

```xml
    <xs:annotation>
        <xs:documentation>
            Ink/Toner Color Representation definition
            A 6-digit hex representation of the RGB color value this Consumable entry represents.
            Examples of these values are:
                Black – 000000
                Red – FF0000
                White – FFFFFF
                Magenta – FF00FF
                Cyan – 00FFFF
                Yellow – FFFF00
                Blue – 0000FF
        </xs:documentation>    </xs:annotation>
    <xs:element name="ColorRepresentation" type="wprt11:ColorRepType"/>
    <xs:simpleType name="ColorRepType">
        <xs:restriction base="xs:string">
            <xs:length value="6"/>
        </xs:restriction>
    </xs:simpleType>
```

如本主题前面所述，在 "WS 打印版 1.2" 部分，已通过 WS 打印版命名空间引入了以下新操作。

## <a name="setprinterelements"></a>SetPrinterElements

**SetPrinterElements**操作是新操作，可让客户端在打印机上设置架构元素的值。 SetPrinterElements 操作包含八个请求元素和四个响应元素。 Request 和 response 元素使客户端能够在与 WS 打印设备架构连接时对数据插入和检索进行精细控制。

例如，"ElementPath" 数据元素 ("SetPrinterElements") 操作的一部分，它是一个 XPath 字符串，表示要设置的数据元素的打印机架构内的位置。

有关 SetPrinterElements 操作的更多详细信息，请参阅下面 " **下载** " 部分中列出的 "WS 打印" 的支持文件。

## <a name="downloads"></a>下载

### <a name="specification-and-supporting-files-for-ws-print-v10--v12"></a>WS 打印 v1.0-1.2 版的规范和支持文件

**文件：** [设备上 Web 服务的打印设备定义](https://download.microsoft.com/download/E/9/7/E974CFCB-4B3B-40CC-AF92-4F7F84477F0B/Printer.zip)v1.0 
 **说明：** 包含 Microsoft Word 文档和支持文件的 2.64 MB zip 文件;2013年9月16日

### <a name="specification-and-supporting-files"></a>规范和支持文件

**文件：** [设备上 Web 服务的打印设备定义](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PrintDevice.exe)v1.0 
 **说明：** 76 KB 自解压文件，其中包含 Microsoft Word 文档和支持文件;2007年1月29日

**文件：** [在设备上扫描 Web 服务的服务定义](https://download.microsoft.com/download/9/C/5/9C5B2167-8017-4BAE-9FDE-D599BAC8184A/ScanService.zip)v1.0 
 **说明：** (1.5 MB zip 文件，其中包含 Microsoft Word 文档和支持文件;2012年2月9日) 

**文件：** [在设备上扫描设备定义 1.0 for Web 服务](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/ScanDevice.exe) 
 **说明：** (76 KB 自解压文件，其中包含 Microsoft Word 文档和支持文件;2007年1月29日) 

## <a name="related-topics"></a>相关主题

[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)