---
title: 条形码扫描程序蓝牙服务 Uuid
description: 本主题介绍使用蓝牙服务发现协议 (SDP) 与条码扫描器的 Uuid。
ms.assetid: 354654EC-95C8-4BE9-83D3-0926A1E71221
ms.date: 02/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6b6a272f76e803de67fe2d7cd3567e7e07fbddee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520498"
---
# <a name="barcode-scanner-bluetooth-service-uuids"></a>条形码扫描程序蓝牙服务 Uuid

本主题介绍使用蓝牙服务发现协议 (SDP) 与条码扫描器的 Uuid。

## <a name="bluetooth-barcode-scanner-uuids"></a>蓝牙条码扫描器的 Uuid

以下 Uuid 用于标识在发现期间提供的蓝牙条形码扫描程序服务。

### <a name="ssi-service-uuid"></a>SSI 服务 UUID

以下 UUID 标识蓝牙条码扫描器的 SSI 服务。 蓝牙在发现期间公开此 UUID 的设备将被识别为现成驱动程序支持的条形码扫描程序。

```cpp
DEFINE_GUID(BarcodeScannerSimpleSerialInterfaceServiceClass_UUID, 
0xA1220169, 0xE854, 0x473E, 0x9C, 0xB5, 0x87, 0x3A, 0xCB, 0xDF, 0x1F, 0x13)
```

### <a name="reserved-for-future-use"></a>保留供将来使用

以下 UUID 不支持在 Windows 10，版本 1703，但已保留供将来使用 ISCP。

```cpp
DEFINE_GUID(BarcodeScannerIntermecScannerCommunicationProtocolServiceClass_UUID, 
0xccb06baf, 0xdca9, 0x483f, 0x84, 0xd9, 0x36, 0x23, 0x24, 0xce, 0xd, 0x97)
```





