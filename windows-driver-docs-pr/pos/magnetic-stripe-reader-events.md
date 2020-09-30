---
title: 磁条读取器事件
description: 使用 ReadFile 了解从设备驱动程序传递到服务 (POS) API 层的点的磁条读取器事件。
ms.assetid: 48ce9fcb-5ea2-4045-92df-990d94e5e98b
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3b8e8d8c782782610e79dc4d19320d71694dfb92
ms.sourcegitcommit: f1d6c2d0cdbecdc69ba65ed3b530755fc73c8e5e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91590363"
---
# <a name="magnetic-stripe-reader-events"></a>磁条读取器事件

本部分介绍使用 [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 本部分重点介绍特定于磁条纹读取器 (MSRs) 的事件。

## <a name="in-this-section"></a>在此部分中

[MagneticStripeReaderDataReceived](magneticstripereaderdatareceived.md)  
在成功扫描事件之后发生。

[MagneticStripeReaderErrorOccured](magneticstripereadererroroccured.md)  
出现 MSR 错误（如扫描错误）时发生。