---
title: 查看测试证书
description: 查看测试证书
keywords:
- 驱动程序签名 WDK，查看测试证书
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8eb56347be9ef09aefa673228f070f3cbc66b2e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819533"
---
# <a name="viewing-test-certificates"></a>查看测试证书


创建证书并将副本放入证书存储区后，可以使用 Microsoft 管理控制台 (MMC) 证书管理单元来查看该证书。 执行以下操作以通过 MMC " **证书** " 管理单元查看证书：

1.  单击 " **开始** "，然后单击 "开始搜索"。

2.  若要启动 "证书" 管理单元，请键入 Certmgr.msc，然后按 **enter** 键。

3.  在 "证书" 管理单元的左窗格中，展开 "PrivateCertStore" 证书存储文件夹，然后双击 "证书"。

以下屏幕截图显示了 **PrivateCertStore** 证书存储文件夹的 "证书" 管理单元视图。

![显示测试证书的证书存储的屏幕截图 ](images/certstore.png)

若要查看有关 Contoso.com (测试) 证书的详细信息，请在右窗格中双击该证书。 以下屏幕截图显示了有关证书的详细信息。

![显示 contoso.com (test) 证书详细信息的证书窗口的屏幕截图](images/certinfo.png)

请注意，"证书" 对话框状态： "此 CA 根证书不受信任。 若要启用信任，请在受信任的根证书颁发机构存储中安装此证书。 " 这是预期的行为。 无法验证证书，因为 Windows 不信任证书颁发机构，默认情况下，"Contoso.com (Test) "。

 

 





