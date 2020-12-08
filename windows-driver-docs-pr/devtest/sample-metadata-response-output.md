---
title: 示例元数据响应输出
description: 示例元数据响应输出
keywords:
- WSDBIT 工具 WDK，示例
- WSDAPI 基本互操作性工具 WDK，示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06114a7c349d100c8b928dced9711a332e0d5f2e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838339"
---
# <a name="sample-metadata-response-output"></a>示例元数据响应输出

如果 \_ 将 wsdbit 客户端与 wsdbit \_ 服务器一起使用，以下代码示例将显示客户端上的元数据响应输出的外观。

>[!NOTE]
>每次运行服务器时，主机地址终结点都将不同。

```command
-Dialect:       http://schemas.xmlsoap.org/ws/2006/02/devprof/ThisDevice
Device Metadata
        -FriendlyName [-----]: WSDAPI Basic Interop Server
        -FirmwareVersion:      alpha
        -SerialNumber:         1
        -Any:                  (absent)
End Device Metadata
-Dialect:       http://schemas.xmlsoap.org/ws/2006/02/devprof/ThisModel
Model Metadata
        -Manufacturer [-----]: Microsoft
        -ManufacturerURL:      http://www.microsoft.com/
        -ModelName [-----]:    WSDAPI Interop device
        -ModelNumber:          0.1
        -ModelUrl:             http://www.microsoft.com/
        -PresentationUrl:      http://www.microsoft.com/
        -Any:                  (absent)
End Model Metadata
-Dialect:       http://schemas.xmlsoap.org/ws/2006/02/devprof/Relationship
Relationship Metadata
        -Type:        http://schemas.xmlsoap.org/ws/2006/02/devprof/host
        -Host:
         -Address:     urn:uuid:697f393a-c45f-4bd7-9a57-0990344e4037
         -ServiceId:   http://testdevice.interop/SimpleDevice
         -Type: http://schemas.example.org/SimpleService:SimpleDeviceType
         -Any:         (absent)
        -Hosted[0]:
         -Address:     http://[::1]:5357/697f393a-c45f-4bd7-9a57-0990344e4037
         -Address:     http://127.0.0.1:5357/697f393a-c45f-4bd7-9a57-0990344e4037
         -ServiceId:   http://testdevice.interop/SimpleService1
         -Type: http://schemas.example.org/SimpleService:SimpleService
         -Any:         (absent)
        -Hosted[1]:
         -Address:     http://[::1]:5357/697f393a-c45f-4bd7-9a57-0990344e4037
         -Address:     http://127.0.0.1:5357/697f393a-c45f-4bd7-9a57-0990344e4037
         -ServiceId:   http://testdevice.interop/AttachmentService1
         -Type: http://schemas.example.org/AttachmentService:AttachmentService
         -Any:         (absent)
        -Hosted[2]:
         -Address:     http://[::1]:5357/697f393a-c45f-4bd7-9a57-0990344e4037
         -Address:     http://127.0.0.1:5357/697f393a-c45f-4bd7-9a57-0990344e4037
         -ServiceId:   http://testdevice.interop/EventingService1
         -Type: http://schemas.example.org/EventingService:EventingService
         -Any:         (absent)
End Relationship Metadata
```
