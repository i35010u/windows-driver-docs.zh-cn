---
title: 安装适用于非 PnP 驱动程序且已进行发布签名的目录文件
description: 安装适用于非 PnP 驱动程序且已进行发布签名的目录文件
ms.assetid: a67f3b71-b7a6-4712-a76f-b3b412a149c2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5893789273a46615f428b354d3eadbe63f56b36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565837"
---
# <a name="installing-a-release-signed-catalog-file-for-a-non-pnp-driver"></a>安装适用于非 PnP 驱动程序且已进行发布签名的目录文件


若要符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)的 64 位版本的 Windows Vista 和更高版本的 Windows，非启动，非 PnP 内核模式驱动程序必须具有嵌入的版本签名或已发布签名[编录文件](catalog-files.md)安装在系统组件和驱动程序数据库中。 此外，如果使用版本签名的目录文件进行身份验证的用户模式驱动程序或 32 位非 PnP 内核模式驱动程序，Windows 代码签名策略要求的编录文件安装在系统组件和驱动程序数据库中。 即插即用设备安装会自动安装驱动程序数据库中的即插即用驱动程序的目录文件。 但是，对于非 PnP 驱动程序安装的非 PnP 驱动程序的安装应用程序必须安装目录文件驱动程序数据库中。

若要安装到公共非 PnP 驱动程序一起发布的目录文件，可再发行组件安装应用程序应使用[CryptCATAdminAddCatalog](https://go.microsoft.com/fwlink/p/?linkid=104926)加密函数，如中所述[安装通过使用 CryptCATAdminAddCatalog 目录文件](installing-a-catalog-file-by-using-cryptcatadminaddcatalog.md)。

**请注意**  一般情况下，不能使用可再发行组件安装应用程序[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)工具安装目录文件，因为 SignTool 不是可再发行组件的工具.

 

**提示**  使用嵌入式的签名是通常会更简单、 更高效比使用签名的编录文件。 有关使用嵌入式的签名与签名的编录文件的优缺点的详细信息，请参阅[测试签名驱动程序](https://msdn.microsoft.com/windows-drivers/develop/signing_a_driver)。

 

 

 





