---
title: 条形码扫描仪蓝牙服务 UUID
description: 本主题介绍与用于条形码扫描器 (SDP) 的蓝牙服务发现协议一起使用的 Uuid。
ms.date: 02/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5b68942ba8eba34a6927705aa4804f71b746fe6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806043"
---
# <a name="barcode-scanner-bluetooth-service-uuids"></a>条形码扫描仪蓝牙服务 UUID

本主题介绍与用于条形码扫描器 (SDP) 的蓝牙服务发现协议一起使用的 Uuid。

## <a name="bluetooth-barcode-scanner-uuids"></a>蓝牙条形码扫描仪 UUID

以下 Uuid 用于标识蓝牙条形码扫描器在发现过程中提供的服务。

### <a name="ssi-service-uuid"></a>SSI 服务 UUID

以下 UUID 标识蓝牙条形码扫描器的 SSI 服务。 在蓝牙发现期间公开此 UUID 的设备将被识别为内置驱动程序支持的条形码扫描仪。

```cpp
DEFINE_GUID(BarcodeScannerSimpleSerialInterfaceServiceClass_UUID, 
0xA1220169, 0xE854, 0x473E, 0x9C, 0xB5, 0x87, 0x3A, 0xCB, 0xDF, 0x1F, 0x13)
```

### <a name="reserved-for-future-use"></a>保留以供将来使用

Windows 10 版本1703不支持以下 UUID，但保留该 UUID 供将来用于 ISCP。

```cpp
DEFINE_GUID(BarcodeScannerIntermecScannerCommunicationProtocolServiceClass_UUID, 
0xccb06baf, 0xdca9, 0x483f, 0x84, 0xd9, 0x36, 0x23, 0x24, 0xce, 0xd, 0x97)
```





