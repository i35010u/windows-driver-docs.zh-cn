---
title: 示例元数据响应输出
description: 示例元数据响应输出
ms.assetid: e31cdc1f-21eb-4121-9618-2d8e3d6775dc
keywords:
- WSDBIT 工具 WDK 示例
- WSDAPI 基本互操作性工具 WDK 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce9c588a1e963f18d09e0c6832e8a1a5824e4aaa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568900"
---
# <a name="sample-metadata-response-output"></a>示例元数据响应输出


如果 wsdbit\_客户端所用 wsdbit\_服务器，下面的代码示例显示了客户端上的元数据响应输出将如下所示。

**请注意**  每次运行服务器时，将不同主机地址终结点。

 

```
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

 

 





