---
title: WS-Discovery 移动打印支持
description: WS-Discovery 移动打印支持
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8da956024da9b72b0a603bd912c9e237de5bfef3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831175"
---
# <a name="ws-discovery-mobile-printing-support"></a>WS-Discovery 移动打印支持

支持从 Windows 10 移动版打印的设备，必须将 MobilePrinter 类别添加到其 WS-Discovery ThisModel 响应中，如以下示例中所示：

```xml
<soap:Envelope
    xmlns:soap="https://www.w3.org/2003/05/soap-envelope"
    xmlns:wsa="https://schemas.xmlsoap.org/ws/2004/08/addressing"
    xmlns:wsdisco="https://schemas.xmlsoap.org/ws/2005/04/discovery"
    xmlns:wsx="https://schemas.xmlsoap.org/ws/2004/09/mex"
    xmlns:wsd="https://schemas.xmlsoap.org/ws/2006/02/devprof"
    xmlns:pnpx="https://schemas.microsoft.com/windows/pnpx/2005/10">

    <soap:Header>
        <!-- Place SOAP header information here.-->
    </soap:Header>

    <soap:Body>
        <wsx:Metadata>
            <wsx:MetadataSection
                Dialect="https://schemas.xmlsoap.org/ws/2005/05/devprof/ThisDevice">
                <wsd:ThisDevice>
                    <!-- Place ThisDevice metadata here.-->
                </wsd:ThisDevice>
            </wsx:MetadataSection>

           <wsx:MetadataSection
                Dialect="https://schemas.xmlsoap.org/ws/2005/05/devprof/ThisModel">
                <wsd:ThisModel>
                    <!-- Place ThisModel metadata here.-->
                    <pnpx:DeviceCategory>
                        <!-- This device is in the Printers category -->
                        Printers Scanners MobilePrinter
                   </pnpx:DeviceCategory>
                </wsd:ThisModel>
            </wsx:MetadataSection>  

            <wsx:MetadataSection
                Dialect="https://schemas.xmlsoap.org/ws/2005/05/devprof/Relationship">
                <wsd:Relationship
                    Type="https://schemas.xmlsoap.org/ws/2005/05/devprof/host">

                    <wsd:Hosted>
                        <!-- Place Hosted metadata for the 
                             first service here.-->
                        <pnpx:HardwareId>
                            <!-- Place the Hardware ID for the first service here.-->
                            PnPX_SampleService1_HWID
                        </pnpx:HardwareId>
                        <pnpx:CompatibleId>
                            <!-- Place the Compatible ID for the first service here.-->
                            PnPX_SampleService1_CPID
                        </pnpx:CompatibleId>
                    </wsd:Hosted>

                </wsd:Relationship>
            </wsx:MetadataSection>

        </wsx:Metadata>
    </soap:Body>
</soap:Envelope>
```

下表提供了有关 MobilePrinter category 关键字的其他信息：

| 常量/值 | 描述 |
|--|--|
| PNPX_DEVICECATEGORY_PRINTER_MOBILE<br><br>L "MobilePrinter" | MobilePrinter 类别<br><br>关键字：打印机 |

有关如何将设备类别添加到 WS-Discovery 元数据交换的详细信息，请参阅 [pnp-x 规范](/previous-versions/gg463082(v=msdn.10))。
