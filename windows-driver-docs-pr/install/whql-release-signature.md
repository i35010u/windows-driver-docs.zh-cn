---
title: WHQL 发布签名
description: WHQL 发布签名
ms.assetid: edc815d4-596c-4f50-9bff-029b8ea19a0a
keywords:
- 驱动程序签名 WDK，WHQL 数字签名
- 对驱动程序进行签名 WDK，WHQL 数字签名
- 数字签名 WDK，WHQL
- 签名 WDK，WHQL
- WHQL 数字签名 WDK
- 公共版本驱动程序签名 WDK，WHQL
- release 签名 WDK，WHQL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1576cbb130f4958b5dc0c776510246dad6041e65
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094807"
---
# <a name="whql-release-signature"></a>WHQL 发布签名


通过 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) 测试的[驱动程序包](driver-packages.md)可以由 WHQL 进行数字签名。 如果你的驱动程序包已由 WHQL 进行数字签名，则可以通过 [Windows 更新](/windows-hardware/drivers) 程序或其他 Microsoft 支持的分发机制来分发。

获取 WHQL 发布签名是 [Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893) 的一部分。 WHQL 发布签名包含经过数字签名的[目录文件](catalog-files.md)。 数字签名不会更改你提交用于测试的驱动程序二进制文件或 INF 文件。

获取 WHQL 版本签名由以下内容组成：

-   用 Windows HCK 测试 [驱动程序包](driver-packages.md) ，验证驱动程序包是否与 Microsoft Windows 兼容。 安装 HCK 后，将运行测试管理器 (DTM) 的驱动程序来测试和验证驱动程序包。 有关详细信息，请参阅 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?linkid=254893)。

-   将 DTM 测试日志提交给 Windows 优质 Online Services，以获取驱动程序包的 WHQL 版本签名。 有关详细信息，请参阅 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?linkid=254893)。

有关 WHQL 的详细信息，请参阅 [Windows 硬件质量实验室](https://go.microsoft.com/fwlink/p/?linkid=8705) 网站。

**注意**   WHQL 不会将签名嵌入驱动程序文件。 你可以使用第三方商业 [版证书](release-certificates.md)将签名嵌入驱动程序文件。 在将驱动程序包提交给 WHQL 之前，将签名嵌入驱动程序文件。

 

 

