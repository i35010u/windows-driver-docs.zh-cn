---
title: POS 设备驱动程序设计指南
description: 本部分提供了服务点 (POS) 设备驱动程序的设计指南。
ms.assetid: D00B2CDF-C5CB-4CB5-A6AE-ECDE52B7603B
ms.date: 09/07/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 68a0208f6b1ffec3db71e05bb2221b806c6a43b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843575"
---
# <a name="pos-device-driver-design-guide"></a>POS 设备驱动程序设计指南

本部分提供了服务点 (POS) 设备的驱动程序设计指南。

## <a name="in-this-section"></a>本部分内容

| 主题 | 描述 |
| --- | --- |
| [POS 驱动程序示例](driver-samples.md) | 提供了演示如何为服务点 (POS) 设备创建通用驱动程序的示例。 |
| [条形码扫描仪蓝牙服务 UUID](barcode-scanner-bluetooth-service-uuids.md) | 介绍了用于条形码扫描仪的蓝牙服务发现协议 (SDP) 的 UUID。 |
| [条形码扫描仪事件](barcode-scanner-events.md) | 介绍了特定于条形码扫描仪的事件。 |
| [磁条读取器事件](magnetic-stripe-reader-events.md) | 介绍了特定于磁条读取器 (MSR) 的事件。 |
| [POS 事件](pos-events.md) | 介绍了从设备驱动程序传递到 POS API 层的一般 POS 事件。 |

## <a name="related-sections"></a>相关章节

[POS DDI 参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_pos)
