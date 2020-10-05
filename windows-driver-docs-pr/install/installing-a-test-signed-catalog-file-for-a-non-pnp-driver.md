---
title: 安装适用于非 PnP 驱动程序且已进行测试签名的目录文件
description: 安装适用于非 PnP 驱动程序且已进行测试签名的目录文件
ms.assetid: 8586bacc-86c5-4402-84fa-6f1efe967f5d
keywords:
- 测试签名驱动程序包 WDK，编录文件
- CAT 文件
- .cat 文件
- 非 PnP 驱动程序目录文件 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48bbcc04e8ac97fd26b6e4264fb6d9af790bc1f6
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733957"
---
# <a name="installing-a-test-signed-catalog-file-for-a-non-pnp-driver"></a>安装适用于非 PnP 驱动程序且已进行测试签名的目录文件


若要符合64位版本的 Windows Vista 和更高版本的 Windows 的 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) ，非启动、非 PnP 驱动程序必须在系统组件和驱动程序数据库中具有嵌入签名或已签名的 [目录文件](catalog-files.md) 。 PnP 设备安装会在驱动程序数据库中自动安装 PnP 驱动程序的编录文件。 但是，对于非 PnP 驱动程序，安装非 PnP 驱动程序的安装应用程序必须在驱动程序数据库中安装目录文件。

驱动程序安装应用程序可以通过使用 [CryptCATAdminAddCatalog](/windows/win32/api/mscat/nf-mscat-cryptcatadminaddcatalog) 加密函数以编程方式在系统组件和驱动程序数据库中安装目录文件。 如果应用程序是可再发行的，则应使用此方法安装目录文件。 有关此方法的详细信息，请参阅 [使用 CryptCATAdminAddCatalog 安装目录文件](installing-a-catalog-file-by-using-cryptcatadminaddcatalog.md)。

或者，你可以使用 [**SignTool**](../devtest/signtool.md) 工具在系统组件和驱动程序数据库中安装 [目录文件](catalog-files.md) 。 不过，SignTool 不是可再发行的工具。 因此，仅当已在计算机上安装了该工具时，安装应用程序才能在计算机上使用 SignTool，这种方式符合该工具的 Microsoft 软件许可条款。 有关此方法的详细信息，请参阅 [使用 SignTool 安装目录文件](installing-a-catalog-file-by-using-signtool.md)。

**提示**   使用嵌入的签名通常比使用已签名的目录文件更简单、更有效。 有关使用嵌入的签名与签名的目录文件的优点和缺点的详细信息，请参阅对 [驱动程序进行测试签名](/windows-hardware/drivers)。

 

