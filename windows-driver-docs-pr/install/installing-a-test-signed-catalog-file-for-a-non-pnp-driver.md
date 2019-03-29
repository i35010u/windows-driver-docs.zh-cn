---
title: 安装适用于非 PnP 驱动程序且已进行测试签名的目录文件
description: 安装适用于非 PnP 驱动程序且已进行测试签名的目录文件
ms.assetid: 8586bacc-86c5-4402-84fa-6f1efe967f5d
keywords:
- 测试签名驱动程序包 WDK，目录文件
- CAT 文件
- .cat 文件
- 非 PnP 驱动程序目录文件 WDK 驱动程序签名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2eeda8449a05d88479ee660ffa9297c51ad6c9e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567150"
---
# <a name="installing-a-test-signed-catalog-file-for-a-non-pnp-driver"></a>安装适用于非 PnP 驱动程序且已进行测试签名的目录文件


若要符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)64 位版本的 Windows Vista 和更高版本的 Windows，非启动，非 PnP 驱动程序必须具有嵌入式的签名或签名[目录文件](catalog-files.md)安装在系统组件和驱动程序数据库中。 即插即用设备安装会自动安装驱动程序数据库中的即插即用驱动程序的目录文件。 但是，对于非 PnP 驱动程序安装的非 PnP 驱动程序的安装应用程序必须安装目录文件驱动程序数据库中。

驱动程序安装应用程序可以以编程方式来安装目录文件在系统组件和驱动程序数据库中使用[CryptCATAdminAddCatalog](https://go.microsoft.com/fwlink/p/?linkid=104926)加密函数。 如果应用程序是可再发行组件，应使用这种方法来安装目录文件。 有关此方法的详细信息，请参阅[使用 CryptCATAdminAddCatalog 安装目录文件](installing-a-catalog-file-by-using-cryptcatadminaddcatalog.md)。

或者，可以使用[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)要安装的工具[编录文件](catalog-files.md)系统组件和驱动程序数据库中。 但是，SignTool 不是可再发行组件的工具。 因此，安装应用程序可以使用 SignTool 的计算机上才符合该工具 Microsoft 软件许可条款的方式在计算机上已安装该工具。 有关此方法的详细信息，请参阅[安装目录文件使用 SignTool](installing-a-catalog-file-by-using-signtool.md)。

**提示**  使用嵌入式的签名是通常会更简单、 更高效比使用签名的编录文件。 有关使用嵌入式的签名与签名的编录文件的优缺点的详细信息，请参阅[测试签名驱动程序](https://msdn.microsoft.com/windows-drivers/develop/signing_a_driver)。

 

 

 





