---
title: 本地计算机和当前用户证书存储
description: 本地计算机和当前用户证书存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42168999dcc339df0a77983dd3bcb668e0cdce27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808699"
---
# <a name="local-machine-and-current-user-certificate-stores"></a>本地计算机和当前用户证书存储


每个系统证书存储具有以下类型：

* 本地计算机证书存储

    这种类型的证书存储是计算机的本地证书存储，并且对于计算机上的所有用户都是全局性的。 此证书存储位于注册表中 HKEY_LOCAL_MACHINE 根下。

* 当前用户证书存储

    此类型的证书存储区是计算机上用户帐户的本地证书。 此证书存储位于注册表中 HKEY_CURRENT_USER 根下。

有关证书存储的特定注册表位置，请参阅 [系统存储位置](/windows/desktop/seccrypto/system-store-locations)。

请注意，当前 *用户/个人存储区之外* 的所有当前用户证书存储都将继承本地计算机证书存储的内容。 例如，如果将证书添加到本地计算机的 " [受信任的根证书颁发机构" 证书存储](trusted-root-certification-authorities-certificate-store.md)中，则所有当前用户受信任的根证书颁发机构证书存储 (，并附带上述注意事项) 也包含证书。

>[!NOTE]
>即插即用 (PnP) 安装期间的驱动程序签名验证要求根证书和 Authenticode 证书（包括 [测试证书](./makecert-test-certificate.md)）位于本地计算机证书存储中。

 

有关如何在系统证书存储中添加或删除证书的详细信息，请参阅 [**certmgr.msc**](../devtest/certmgr.md)。

 

