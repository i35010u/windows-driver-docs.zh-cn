---
title: 发布证书
description: 发布证书
keywords:
- 公共版本驱动程序签名 WDK，发行证书
- 发布签名 WDK，发布证书
- 发布证书 WDK
- 证书 WDK，发行版
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9d13217500bb6cad3f9c7d5449ce12553eee2e1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833487"
---
# <a name="release-certificates"></a>发布证书


若要符合64位版本的 Windows Vista 和更高版本的 Windows 的内核模式代码签名策略，你必须获取[WHQL 版本签名](whql-release-signature.md)，或使用[ (SPC) 的软件发行者证书](software-publisher-certificate.md)对内核模式[驱动程序包](driver-packages.md)的[目录文件](catalog-files.md)进行签名。

如果驱动程序是适用于64位系统的 *引导启动驱动* 程序，则还必须将 SPC 签名 [嵌入](embedded-signatures-in-a-driver-file.md) 驱动程序文件。 这适用于任何类型的即插即用 (PnP) 或非 PnP 内核模式驱动程序。

[硬件认证工具包 (HCK) ](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))包含各种设备类型的[测试类别](/windows-hardware/test/hlk/)。 若要符合 Windows Vista 和更高版本的 windows Vista 和更高版本的 [PnP 设备安装32要求](pnp-device-installation-signing-requirements--windows-vista-and-later-.md) ，如果 HCK 具有设备类型的测试类别，则应该获取 WHQL 版本签名。 如果无法获取 WHQL 版本签名，则必须使用 SPC 或 [商业发行版证书](commercial-release-certificate.md) 为 PnP 内核模式驱动程序签名。

 

