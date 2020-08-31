---
title: 即插即用设备安装签名要求
description: 即插即用设备安装签名要求
ms.assetid: 92527b24-b29a-4a78-886d-fafd620090d1
keywords:
- 驱动程序签名 WDK，PnP 设备安装
- 对驱动程序进行签名 WDK，PnP 设备安装
- 数字签名 WDK，PnP 设备安装
- 签名 WDK，PnP 设备安装
- PnP WDK 驱动程序签名
- 即插即用 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d364570c0d13fd36abf8770a4c084342091d2b5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094863"
---
# <a name="pnp-device-installation-signing-requirements"></a>即插即用设备安装签名要求

即插即用 (PnP) 设备安装的驱动程序签名要求取决于 Windows 的版本，以及在开发和测试驱动程序的过程中是否对驱动程序进行公共版本或开发团队签名。 所有64位版本的 Windows 都强制执行 [内核模式代码签名要求](kernel-mode-code-signing-requirements--windows-vista-and-later-.md) ，这些要求确定是否可以加载内核模式驱动程序。

## <a name="pnp-signing-requirements-for-public-release-of-a-driver"></a><a href="" id="pnp-signing-requirements-for-public-release-of-a-driver"></a> 公共版本驱动程序的 PnP 签名要求

[Windows 硬件实验室工具包 (WINDOWS HLK) ](/windows-hardware/test/hlk/windows-hardware-lab-kit)具有各种设备类型的[测试类别](/windows-hardware/test/hlk/testref/hardware-lab-kit-test-reference)。 如果此列表中包含设备类型的测试类别，你应该获得 [WHQL 版本签名](whql-release-signature.md)。

有效的 WHQL 版本签名验证驱动程序是否符合 HCK 要求，验证发布服务器的身份，并验证驱动程序是否未被更改。

若要被 PnP 设备安装所签署，[驱动程序包](driver-packages.md)的[编录文件](catalog-files.md)必须由 WHQL 签署，或由第三方[版本证书](release-certificates.md)签名 ([软件发行者证书 (SPC) ](software-publisher-certificate.md)或商业版本证书) 。 如果可以获取 WHQL 版本签名，则应使用该签名。 第三方版本签名验证发布服务器的身份，并且驱动程序未被更改。 但是，与 WHQL 版本签名不同，第三方版本签名不会验证驱动程序功能。

另请注意，对于64位版本的 Windows Vista 和更高版本的 Windows，内核模式代码签名策略会进一步要求 WHQL 或 SPC 对内核模式驱动程序进行签名。

有关发布签名的详细信息，请参阅 [为公共版本签署驱动程序](signing-drivers-for-public-release--windows-vista-and-later-.md)。

## <a name="pnp-signing-requirements-for-development-and-test-of-a-driver"></a><a href="" id="pnp-signing-requirements-for-development-and-test-of-a-driver"></a> 用于开发和测试驱动程序的 PnP 签名要求

在 Windows Vista 和更高版本的 windows 的64位版本中，驱动程序必须具有 [WHQL 测试签名](whql-test-signature-program.md) ，或者必须由 [测试证书](./makecert-test-certificate.md)签名。 有关测试签名驱动程序的详细信息，请参阅 [在开发和测试期间对驱动程序进行签名](./introduction-to-test-signing.md)。