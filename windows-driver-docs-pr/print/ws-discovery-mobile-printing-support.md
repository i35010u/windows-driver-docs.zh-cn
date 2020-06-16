---
title: WS-Discovery 移动打印支持
description: WS-Discovery 移动打印支持
ms.assetid: 788E2A1C-FBE9-40CD-A3EB-14A2DE266A2C
ms.date: 06/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: b053377542cba980c97f3cbb41ff9ec1838466b8
ms.sourcegitcommit: 77c63789350cfc1dc740baaafdef64803d86217f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84793743"
---
# <a name="ws-discovery-mobile-printing-support"></a>WS-Discovery 移动打印支持

支持从 Windows 10 移动版打印的设备必须将 MobilePrinter 类别添加到其 WS-RELIABLEMESSAGING ThisModel 响应中，如以下示例中所示：

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

| 常量/值 | 说明 |
|--|--|
| PNPX_DEVICECATEGORY_PRINTER_MOBILE<br><br>L "MobilePrinter" | MobilePrinter 类别<br><br>关键字：打印机 |

有关如何将设备类别添加到 WS 发现元数据交换的详细信息，请参阅[pnp-x 规范](https://docs.microsoft.com/previous-versions/gg463082(v=msdn.10))。
