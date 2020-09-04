---
title: 指纹度量值
description: 指纹度量查看使用指纹设备的用户体验的成功情况
ms.topic: article
ms.date: 03/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: 1031fb4b23173ffe3db03b58d73f168675ab72e4
ms.sourcegitcommit: 4f08f5686c0bbc27d58930b993cbab1a98e3afb0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89443733"
---
# <a name="fingerprint-measures"></a>指纹度量值

## <a name="description"></a>说明

[Windows 生物识别框架 (WBF)](/windows/win32/secbiomet/biometric-service-api-portal) 为要与 Windows 10 集成的生物识别传感器提供了一个可插入模型。 插入到 WBF 中的指纹传感器将作为 Windows Hello 的一部分向用户公开。 指纹传感器可通过实现一个使用 [Windows 生物识别驱动程序接口 (WBDI)](../biometric/index.md) 的用户模式驱动程序，来向框架注册。 驱动程序中包含的适配器使 WBF 可以调用传感器来协调生物识别操作，包括捕获样本、匹配操作和模板管理操作。