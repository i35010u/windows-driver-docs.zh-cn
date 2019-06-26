---
title: 本地计算机和当前用户证书存储
description: 本地计算机和当前用户证书存储
ms.assetid: b7362f2e-c8ff-42e4-9edc-df4b9967df29
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e6551bb13f2cdfdb4ed53b882a17638f961506a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377671"
---
# <a name="local-machine-and-current-user-certificate-stores"></a>本地计算机和当前用户证书存储


每个系统证书存储具有以下类型：

* 本地计算机证书存储

    这种类型的证书存储区是计算机的本地和适用的计算机上的所有用户。 此证书存储区位于在注册表中 HKEY_LOCAL_MACHINE 根下。

* 当前用户证书存储区

    这种类型的证书存储是本地的计算机上的用户帐户。 此证书存储区位于在 HKEY_CURRENT_USER 根目录下的注册表中。

有关特定注册表的证书存储位置，请参阅[系统存储位置](https://docs.microsoft.com/windows/desktop/seccrypto/system-store-locations)。

请注意，所有当前用户的证书存储*除非当前用户/个人存储区*继承本地计算机证书存储的内容。 例如，如果将证书添加到本地计算机[受信任的根证书颁发机构证书存储区](trusted-root-certification-authorities-certificate-store.md)，所有当前用户 （具有更高版本需要注意的地方） 也受信任的根证书颁发机构证书存储。包含证书。

>[!NOTE]
>驱动程序签名验证在插即用 (PnP) 安装过程中需要该根和验证码证书，包括[测试证书](test-certificates.md)，位于本地计算机证书存储中。

 

有关如何添加或从系统证书存储中删除证书的详细信息，请参阅[ **CertMgr**](https://docs.microsoft.com/windows-hardware/drivers/devtest/certmgr)。

 

 





