---
title: 发布证书
description: 发布证书
ms.assetid: 61bd5002-b3b6-4f11-b0c2-80eeaf2fec39
keywords:
- 公开发布的版本驱动程序签名 WDK，发布证书
- 释放签名 WDK，发布证书
- 发布证书 WDK
- 证书 WDK，发布
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0aeb74c1ab2cb88a51cd779948026e77b9b0dc4f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348177"
---
# <a name="release-certificates"></a>发布证书


若要符合内核模式代码签名的 64 位版本的 Windows Vista 和更高版本的 Windows 的策略，你必须获取[WHQL 版本签名](whql-release-signature.md)或使用[软件发行者证书 (SPC)](software-publisher-certificate.md)进行签名[编录文件](catalog-files.md)的内核模式[驱动程序包](driver-packages.md)。

如果驱动程序*引导启动驱动程序*对于 64 位系统，您还必须[嵌入](embedded-signatures-in-a-driver-file.md)驱动程序文件中的 SPC 签名。 这适用于任何类型的插 (PnP) 或非 PnP 内核模式驱动程序。

[硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)已[测试类别](https://go.microsoft.com/fwlink/p/?linkid=189178)多种设备类型。 若要符合[PnP 设备安装要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md)的 32 位版本的 Windows Vista 和更高版本的 Windows，你应获取 WHQL 版本签名，如果该 HCK 提供的设备类型的测试类别。 如果您不能获得 WHQL 版本签名，则必须使用任一一个 SPC 或[商业版本发布证书](commercial-release-certificate.md)进行签名的即插即用的内核模式驱动程序。

 

 





