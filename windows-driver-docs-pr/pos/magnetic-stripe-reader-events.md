---
title: 磁条读取器事件
description: 使用 ReadFile 描述从设备驱动程序传递到服务 (POS) API 层的点的事件。
ms.assetid: 48ce9fcb-5ea2-4045-92df-990d94e5e98b
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: c8516c269eb19e8c0697599cd5871218d4faaec5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191919"
---
# <a name="magnetic-stripe-reader-events"></a>磁条读取器事件

本部分介绍使用 [ReadFile](/windows/desktop/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 本部分重点介绍特定于磁条纹读取器 (MSRs) 的事件。

## <a name="in-this-section"></a>本节内容

[MagneticStripeReaderDataReceived](magneticstripereaderdatareceived.md)  
在成功扫描事件之后发生。

[MagneticStripeReaderErrorOccured](magneticstripereadererroroccured.md)  
出现 MSR 错误（如扫描错误）时发生。