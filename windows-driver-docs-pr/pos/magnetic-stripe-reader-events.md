---
title: 磁条读取器事件
description: 使用 ReadFile 了解从设备驱动程序传递到服务 (POS) API 层的点的磁条读取器事件。
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 74378be8021c0e8c04dec609a1b4c53eb8c1ee4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794313"
---
# <a name="magnetic-stripe-reader-events"></a>磁条读取器事件

本部分介绍使用 [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile)从设备驱动程序传递到服务 (POS) API 层的事件。 本部分重点介绍特定于磁条纹读取器 (MSRs) 的事件。

## <a name="in-this-section"></a>在本节中

[MagneticStripeReaderDataReceived](magneticstripereaderdatareceived.md)  
在成功扫描事件之后发生。

[MagneticStripeReaderErrorOccured](magneticstripereadererroroccured.md)  
出现 MSR 错误（如扫描错误）时发生。
