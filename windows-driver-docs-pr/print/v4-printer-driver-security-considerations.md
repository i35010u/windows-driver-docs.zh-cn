---
title: V4 打印机驱动程序安全注意事项
description: 除了常见的威胁，如特权提升、欺骗设备或注入式攻击，v4 打印机驱动程序还需要与低权限应用程序兼容。
ms.assetid: 8A1508C1-4856-4E3C-8378-AC5FDD55D118
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 278aeabac863c9a81a0c4c98188299d0607c348b
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534936"
---
# <a name="v4-printer-driver-security-considerations"></a>V4 打印机驱动程序安全注意事项

除了常见的威胁，如特权提升、欺骗设备或注入式攻击，v4 打印机驱动程序还需要与低权限应用程序（例如 Internet Explorer 9）兼容。

XPS 呈现筛选器和 JavaScript 文件必须全部针对跨计算机边界的应用程序、用户或数据中的所有形式的不受信任的数据进行强化。 格式不正确的 Printticket、XPS 文档、属性包甚至 BidiResponses 必须仔细进行验证和分析，并且决不会用于存储可执行代码。 建议合作伙伴使用广泛的模糊文件测试，以确保在不影响安全完整性的情况下正常故障。

## <a name="related-topics"></a>相关主题

[V4 打印机驱动程序开发最佳做法](v4-printer-driver-development-best-practices.md)  
