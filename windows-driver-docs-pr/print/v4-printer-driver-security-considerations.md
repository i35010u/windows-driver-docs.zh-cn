---
title: V4 打印机驱动程序安全注意事项
description: 除了常见的威胁，如提升权限、 欺骗性的设备或拦截式攻击，v4 打印机驱动程序还需要与 Internet Explorer 9 的低权限应用程序兼容。
ms.assetid: 8A1508C1-4856-4E3C-8378-AC5FDD55D118
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf2299bbcf43dd90a02a75ce4ab64059aa280b9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324812"
---
# <a name="v4-printer-driver-security-considerations"></a>V4 打印机驱动程序安全注意事项


除了常见的威胁，如提升权限、 欺骗性的设备或拦截式攻击，v4 打印机驱动程序还需要与 Internet Explorer 9 的低权限应用程序兼容。

XPS 呈现筛选器和 JavaScript 文件必须全部强制写入对所有形式的不受信任的数据从应用程序、 用户或从数据跨计算机界限。 格式不正确的 Printticket、 XPS 文档、 属性包和甚至 BidiResponses 必须验证并仔细分析和应永远不会用来存储可执行代码。 我们建议合作伙伴使用广泛的模糊的文件测试以确保正常的失败不会危及安全完整性。

## <a name="related-topics"></a>相关主题
[V4 打印机驱动程序开发最佳做法](v4-printer-driver-development-best-practices.md)  



