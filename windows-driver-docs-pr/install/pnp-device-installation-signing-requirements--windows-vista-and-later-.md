---
title: 即插即用设备安装签名要求
description: 即插即用设备安装签名要求
ms.assetid: 92527b24-b29a-4a78-886d-fafd620090d1
keywords:
- 驱动程序签名 WDK，即插即用设备安装
- 签署驱动程序 WDK，即插即用设备安装
- 数字签名 WDK，即插即用设备安装
- 签名 WDK，即插即用设备安装
- 即插即用 WDK 驱动程序签名
- 插 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd4a1a3331343f6e07f23973ec5130dd8937b61d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526701"
---
# <a name="pnp-device-installation-signing-requirements"></a>即插即用设备安装签名要求


驱动程序签名要求插即用 (PnP) 设备安装依赖于 Windows 的版本以及是否驱动程序是正被签名的公开发布的版本或由开发团队在开发和测试驱动程序的过程。 所有 64 位版本 Windows 的强制都实施[内核模式代码签名要求](kernel-mode-code-signing-requirements--windows-vista-and-later-.md)，确定是否可以加载的内核模式驱动程序。

### <a href="" id="pnp-signing-requirements-for-public-release-of-a-driver"></a> 驱动程序的公开发布的即插即用签名要求

[硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)已[测试类别](https://go.microsoft.com/fwlink/p/?linkid=189178)多种设备类型。 如果此列表中包含的设备类型的测试类别，你应获取[WHQL 版本签名](whql-release-signature.md)。

有效的 WHQL 版本签名验证驱动程序符合要求的 HCK，验证身份的发布服务器，并验证该驱动程序未更改。

以被视为带符号的即插即用设备安装[编录文件](catalog-files.md)的[驱动程序包](driver-packages.md)必须由 WHQL 签名或由第三方进行签名[发行证书](release-certificates.md)([软件发布者证书 (SPC)](software-publisher-certificate.md)或商业版本发布证书)。 如果可以获取其中一个，则应使用 WHQL 版本签名。 第三方版本签名验证的发布服务器的标识和驱动程序是否已更改。 但是，与 WHQL 版本签名，第三方版本签名不验证驱动程序的功能。

此外请注意，对于 64 位版本的 Windows Vista 和更高版本的 Windows，内核模式代码签名策略进一步要求通过 WHQL 或一个 SPC 进行签名的内核模式驱动程序。

有关版本签名的详细信息，请参阅[签名的驱动程序公共版本](signing-drivers-for-public-release--windows-vista-and-later-.md)。

### <a href="" id="pnp-signing-requirements-for-development-and-test-of-a-driver"></a> 用于开发和测试驱动程序的即插即用签名要求

在 64 位版本的 Windows Vista 和更高版本的 Windows 中，驱动程序必须具有[WHQL 测试签名](whql-test-signature-program.md)或必须由签名[测试证书](test-certificates.md)。 有关测试签名驱动程序的详细信息，请参阅[签名驱动程序开发和测试期间](signing-drivers-during-development-and-test.md)。

 

 





