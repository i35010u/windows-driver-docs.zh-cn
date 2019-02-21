---
title: 用于打印 （WS-打印） 的设备上的 web 服务
description: 有关在 Windows Vista 中，以提供用于打印和扫描外围设备的连接协议引入了打印 （WS-打印） 的 web 服务在设备上。
ms.assetid: 4A641EF8-FBD3-46CA-9284-28AF1A4B8226
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c4afbe76e0f522c62d3785d7b416680503e10b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545588"
---
# <a name="web-services-on-devices-for-printing-ws-print"></a>用于打印 （WS-打印） 的设备上的 web 服务


有关在 Windows Vista 中，以提供用于打印和扫描外围设备的连接协议引入了打印 （WS-打印） 的 web 服务在设备上。

## <a name="overview"></a>概述


Web 服务技术提供了用于描述和共享信息的通用框架。 因此，Windows 附带了一组的使用和控制网络连接的设备上的服务的协议。

四个 Web 服务规范存在用于打印和扫描，以帮助充分利用连接、 安装和使用 Windows 设备时的改进的客户体验的设备制造商。

## <a name="ws-print-v11"></a>WS-Print v1.1


对于 Windows 8，web 服务 (WSD) 的设备上的打印架构已更新到 v1.1。 此版本的架构 （称为 Ws-print v1.1） 已更新为支持增强的驱动程序配置、 更好地颜色墨迹/墨粉量和设备的表示形式模型 Id。

## <a name="ws-print-v12"></a>WS-Print v1.2


对于 Windows 8.1 WS 打印包含所有操作和 Ws-print v1.1 中所用的架构元素，但已更新设备上的 web 服务的打印服务定义。 和用于打印的设备上生成新的 Web 服务是 WS 打印 v1.2。

在新的架构的 WS-打印 v1.2 支持已添加元素和新的操作。 新的架构元素"SupportsWSPrintV12"用于标识对 WS-打印 V1.2 的支持。 新的操作，"SetPrinterElements"允许客户端设置在打印机上的架构元素的值。 例如，客户端可以设置名为打印机将使用要重新对齐喷墨头的"InkHeadAlignmentValue"的自定义元素。

为方便起见，这些规范此处提供了在下载部分中，在完整的独立的窗体，以及其关联 Web 服务描述语言 (WSDLs) 和 XML 架构定义 (Xsd)。 包含的技术文档许可协议，即在引用 Windows 驱动程序开发工具包 (WDK) 包含在这些设备规范的四个 Web 服务。

以下部分提供有关的各个方面的 WS-打印的更多详细的信息。

## <a name="sequence-diagrams"></a>序列图


以下序列图演示客户端与打印机之间的交互以确定 WS 打印命名空间所支持的版本，然后检索扩展的架构元素。

**Ws-print v1.1**。 下面是支持 Ws-print v1.1 的打印机的交互序列图：

![有关 ws 打印 1.1 版支持的交互和为打印机说明和配置的后续查询显示客户端打印机的序列关系图。](images/wsprint-diagv11.png)

如果打印机支持 Ws-print v1.1，然后 GetPrinterElements(wprt:PrinterDescription) 查询响应来自客户端，打印机将发送后的信息，以指示它执行。

打印机确认，它支持 Ws-print v1.1 后，客户端发送 GetPrinterElements(wprt11:DriverConfiguration) 查询，并且打印机的响应的请求驱动程序配置信息。

**WS 打印 v1.2**。 下面是支持 WS-打印 v1.2 的打印机的交互序列图：

![有关 ws 打印 v1.2 支持的交互和为打印机说明和配置的后续查询显示客户端打印机的序列关系图。](images/wsprint-diagv12.png)

如果打印机支持 WS-打印 v1.2，然后 GetPrinterElements(wprt:PrinterDescription) 查询响应来自客户端，打印机将发送后的信息，以指示它执行。

此外打印机应在响应 GetPrinterElements(wprt:PrinterDescription) 调用返回 wprt12:SupportsWSPrintV12。 然后，客户端可以调用 SetPrinterElements 操作 WS 打印设备支持的架构中设置一个或多个数据元素。

打印机确认，它支持 WS-打印 v1.2 后，客户端发送 GetPrinterElements(wprt12:DriverConfiguration) 查询，并且打印机的响应的请求驱动程序配置信息。

## <a name="namespaces"></a>命名空间


**WS-Print v1.1**

**Namespace:**<http://schemas.microsoft.com/windows/2010/06/wdp/printv11>
**XML Namespace 定义：** xmlns:wprt12 ="<http://schemas.microsoft.com/windows/2012/10/wdp/printV12>"

**WS-Print v1.2**

**Namespace:**<http://schemas.microsoft.com/windows/2012/10/wdp/printV12>
**XML Namespace 定义：** xmlns:wprt11 ="<http://schemas.microsoft.com/windows/2010/06/wdp/printv11>"
## <a name="specifying-ws-print-11-support"></a>指定 WS 打印 1.1 支持


支持 WS-打印 1.1 元素的打印机必须更新其 PrinterDescription 包括 wprt11:SupportsWSPrintv11。 如果 wprt11:SupportsWSPrintv11 不是指定并且已设置为 true，WSDMon 将不从打印机请求任何 WS 打印 1.1 元素。

支持 Ws-print v1.1 的打印设备必须在其 PrinterDescription 为了使 Windows 为该命名空间中的任何其他元素的查询中包括以下内容。

```xml
<soap:Envelope
...
  xmlns:wprt11="http://schemas.microsoft.com/windows/2010/06/wdp/printv11">"
...
  <wprt11:SupportsWSPrintv11>true</wprt11:SupportsWSPrintv11>
...
```

以下 XML 代码段派生自 WSD 打印服务规范 v1.0 中，并且上一节中显示正确地使用了内容。

```xml
<soap:Envelope
        xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
        xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
        xmlns:wprt="http://schemas.microsoft.com/windows/2006/08/wdp/print"
        xmlns:wprt11="http://schemas.microsoft.com/windows/2010/06/wdp/printv11">"
  <soap:Header>
    <wsa:To>http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
    <wsa:Action>
      http://schemas.microsoft.com/windows/2006/08/wdp/print/GetPrinterElementsResponse
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

以下 XML 代码段显示了支持 Ws-print v1.1 的打印设备的架构。

```xml
<xs:schema targetNamespace="http://schemas.microsoft.com/windows/2010/06/wdp/printv11"
           xmlns:wprt11="http://schemas.microsoft.com/windows/2010/06/wdp/printv11"
           xmlns:xs="http://www.w3.org/2001/XMLSchema"
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

## <a name="specifying-ws-print-12-support"></a>指定 WS 打印 1.2 支持


支持 WS-打印 1.2 元素的打印机必须更新其 PrinterDescription 包括 wprtV12:SupportsWSPrintV12。 如果 wprtV12:SupportsWSPrintV12 不是指定并且已设置为 true，WSDMon 将不从打印机请求任何 WS 打印 1.2 元素。

支持 WS-打印 v1.2 的打印设备必须在其 PrinterDescription 为了使 Windows 为该命名空间中的任何其他元素的查询中包括以下内容。

```xml
<soap:Envelope
…
    xmlns:wprtV12="http://schemas.microsoft.com/windows/2012/10/wdp/printV12">
…
    <wprtV12:SupportsWSPrintV12>true</wprtV12:SupportsWSPrintV12>
…
</soap:Envelope>
```

以下 XML 片段派生自 WSD 打印服务规范 v1.2，并显示内容的正确用法了上一节中。

```xml
<soap:Envelope
     xmlns:soap="http://www.w3.org/2003/05/soap-envelope"
     xmlns:wsa="http://schemas.xmlsoap.org/ws/2004/08/addressing"
     xmlns:wprt="http://schemas.microsoft.com/windows/2006/08/wdp/print"
     xmlns:wprtV12="http://schemas.microsoft.com/windows/2012/10/wdp/printV12">
     <soap:Header>
          <wsa:To>http://schemas.xmlsoap.org/ws/2004/08/addressing/role/anonymous</wsa:To>
          <wsa:Action>
               http://schemas.microsoft.com/windows/2006/08/wdp/print/GetPrinterElementsResponse
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

以下三个部分中中的架构示例演示如何使用某些引入的新元素与 Ws-print V1.1。 引入了 Ws-print V1.1 命名空间的所有元素的详细信息，请参阅 WS 打印 1.0 版的支持文件 – v1.2 中列出**下载**部分。

## <a name="enhanced-driver-configuration"></a>增强的驱动程序配置


此架构提供了此设备的特定于设备的 GPD 或 PPD 配置文件。

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

## <a name="device-model-id"></a>设备模型 ID


下面的架构描述的设备，ModelID 和用于进行设备元数据检索。 ModelIDs 的详细信息，请参阅[ModelID 元素](https://msdn.microsoft.com/library/windows/hardware/ff549295.aspx)。

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

## <a name="inktoner-color-representation-value"></a>墨迹/墨粉颜色表示形式值


以下架构检索表示特定墨迹缺墨类型的颜色 RGB 三元组。 此值应为任何墨迹缺墨消费品，若要启用要在应用 UI 中显示的颜色的更好地表示形式指定。

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

在 WS 打印 v1.2 部分中，本主题中前面所述使用 WS 打印 V1.2 命名空间已引入以下新的操作。

## <a name="setprinterelements"></a>SetPrinterElements


"SetPrinterElements"操作新建一个，它允许客户端设置在打印机上的架构元素的值。 SetPrinterElements 操作具有八个请求元素和响应的四个元素。 请求和响应元素提供对数据插入和检索与 WS 打印设备架构进行精细控制的客户端。

例如，ElementPath 数据元素 （SetPrinterElements 操作的一部分） 是一个 XPath 字符串，表示要设置的数据元素内的打印机架构的位置。

有关 SetPrinterElements 操作的更多详细信息，请参阅 WS 打印 v1.0 – v1.2 中的下载部分列出的支持文件。

## <a name="downloads"></a>下载


**规范和支持文件 WS 打印 v1.0 – v1.2**

**文件：**[在设备上打印的 Web 服务的设备定义 V1.0](http://download.microsoft.com/download/E/9/7/E974CFCB-4B3B-40CC-AF92-4F7F84477F0B/Printer.zip)
**说明：** 2.64 MB zip 文件包含 Microsoft Word 文档和支持文件;2013 年 9 月 16日日

**规范和支持文件**

**文件：**[在设备上打印的 Web 服务的设备定义 V1.0](http://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/PrintDevice.exe)
**说明：** 自解压文件包含 Microsoft Word 文档和支持文件; 76 KB2007 年 1 月 29日日

**文件：**[扫描设备上的 Web 服务的服务定义 V1.0](http://download.microsoft.com/download/9/C/5/9C5B2167-8017-4BAE-9FDE-D599BAC8184A/ScanService.zip)
**说明：**（1.5 MB zip 文件包含 Microsoft Word 文档和支持文件;2012 年 2 月 9 日)

**文件：**[扫描的设备上的 Web 服务的设备定义 V1.0](http://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/ScanDevice.exe)
**说明：**(76 KB 自解压文件包含 Microsoft Word 文档和支持文件的文件。2007 年 1 月 29 日)
## <a name="related-topics"></a>相关主题
[V4 打印机驱动程序连接](v4-printer-driver-connectivity.md)  



