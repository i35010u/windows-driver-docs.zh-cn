---
title: 安装适用于非 PnP 驱动程序且已进行发布签名的目录文件
description: 安装适用于非 PnP 驱动程序且已进行发布签名的目录文件
ms.assetid: a67f3b71-b7a6-4712-a76f-b3b412a149c2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b40c34026c8b75df1929643113949b37b0017cf4
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733698"
---
# <a name="installing-a-release-signed-catalog-file-for-a-non-pnp-driver"></a>安装适用于非 PnP 驱动程序且已进行发布签名的目录文件


若要符合64位版本的 Windows Vista 和更高版本的 Windows 的 [内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md) ，非启动、非 PnP 内核模式驱动程序必须具有嵌入的版本签名或安装在系统组件和驱动程序数据库中的已发布签名的 [目录文件](catalog-files.md) 。 此外，如果使用发布签名目录文件对用户模式驱动程序或32位非 PnP 内核模式驱动程序进行身份验证，则 Windows 代码签名策略要求在系统组件和驱动程序数据库中安装目录文件。 PnP 设备安装会在驱动程序数据库中自动安装 PnP 驱动程序的编录文件。 但是，对于非 PnP 驱动程序，安装非 PnP 驱动程序的安装应用程序必须在驱动程序数据库中安装目录文件。

若要为发布到公共的非 PnP 驱动程序安装目录文件，可再发行安装应用程序应使用 [CryptCATAdminAddCatalog](/windows/win32/api/mscat/nf-mscat-cryptcatadminaddcatalog) 加密功能，如 [使用 CryptCATAdminAddCatalog 安装目录文件](installing-a-catalog-file-by-using-cryptcatadminaddcatalog.md)中所述。

**注意**   通常，可再发行安装应用程序不能使用[**SignTool**](../devtest/signtool.md)工具来安装目录文件，因为 SignTool 不是可再发行的工具。

 

**提示**   使用嵌入的签名通常比使用已签名的目录文件更简单、更有效。 有关使用嵌入的签名与签名的目录文件的优点和缺点的详细信息，请参阅对 [驱动程序进行测试签名](/windows-hardware/drivers)。

 

