---
title: 指纹度量值
description: 指纹度量查看使用指纹设备的用户体验的成功情况
ms.topic: article
ms.date: 03/30/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7ab3017b067332260583b3d87f8d8c48431b17ce
ms.sourcegitcommit: 774d42aa3392ae88f4890d901dbd3e8945cb2658
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82139495"
---
# <a name="fingerprint-measures"></a>指纹度量值

## <a name="description"></a>说明

[Windows 生物识别框架 (WBF)](https://docs.microsoft.com/windows/win32/secbiomet/biometric-service-api-portal) 为要与 Windows 10 集成的生物识别传感器提供了一个可插入模型。 插入到 WBF 中的指纹传感器将作为 Windows Hello 的一部分向用户公开。 指纹传感器可通过实现一个使用 [Windows 生物识别驱动程序接口 (WBDI)](https://docs.microsoft.com/windows-hardware/drivers/biometric/) 的用户模式驱动程序，来向框架注册。 驱动程序中包含的适配器使 WBF 可以调用传感器来协调生物识别操作，包括捕获样本、匹配操作和模板管理操作。 