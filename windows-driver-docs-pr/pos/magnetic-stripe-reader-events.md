---
title: 磁条读取器事件
description: 使用 ReadFile 描述从设备驱动程序传递到服务 (POS) API 层的点的事件。
ms.assetid: 48ce9fcb-5ea2-4045-92df-990d94e5e98b
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 814cfb7da982ec89ff618a72fe8beb164be8638a
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715874"
---
# <a name="magnetic-stripe-reader-events"></a>磁条读取器事件

本部分介绍使用 [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 本部分重点介绍特定于磁条纹读取器 (MSRs) 的事件。

## <a name="in-this-section"></a>在本节中

[MagneticStripeReaderDataReceived](magneticstripereaderdatareceived.md)  
在成功扫描事件之后发生。

[MagneticStripeReaderErrorOccured](magneticstripereadererroroccured.md)  
出现 MSR 错误（如扫描错误）时发生。