---
title: WHQL 发布签名
description: WHQL 发布签名
ms.assetid: edc815d4-596c-4f50-9bff-029b8ea19a0a
keywords:
- 驱动程序签名 WDK，WHQL 数字签名
- 签名的驱动程序 WDK、 WHQL 数字签名
- 数字签名 WDK WHQL
- 签名 WDK WHQL
- WHQL 数字签名 WDK
- 公开发布的版本驱动程序签名 WDK，WHQL
- 释放 WDK，WHQL 签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c3e11cec40da6182eb3e5e9e2c2799adfe30875
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363513"
---
# <a name="whql-release-signature"></a>WHQL 发布签名


通过 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) 测试的[驱动程序包](driver-packages.md)可以由 WHQL 进行数字签名。 如果驱动程序包是由 WHQL 进行数字签名，它可以通过分发[Windows Update](https://docs.microsoft.com/windows-hardware/drivers)程序或其他 Microsoft 支持分发机制。

获取 WHQL 发布签名是 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) 的一部分。 WHQL 发布签名包含经过数字签名的[目录文件](catalog-files.md)。 数字签名不更改驱动程序二进制文件或你提交用于测试的 INF 文件。

获取 WHQL 版本签名包括以下：

-   测试[驱动程序包](driver-packages.md)Windows hck 来验证是否与 Microsoft Windows 兼容的驱动程序包。 一旦安装 HCK，驱动程序测试管理器 (DTM) 将运行进行测试和验证驱动程序包。 有关详细信息，请参阅[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)。

-   提交 DTM 测试日志传输到 Windows Quality Online Services，以获取 WHQL 版本签名的驱动程序包。 有关详细信息，请参阅[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)。

有关 WHQL 的详细信息，请参阅[Windows 硬件质量实验室](https://go.microsoft.com/fwlink/p/?linkid=8705)网站。

**请注意**  WHQL 不在驱动程序文件中嵌入签名。 可以使用第三方商业驱动程序文件中嵌入签名[发布证书](release-certificates.md)。 在驱动程序文件中嵌入签名，然后再提交到 WHQL 驱动程序包。

 

 

 





