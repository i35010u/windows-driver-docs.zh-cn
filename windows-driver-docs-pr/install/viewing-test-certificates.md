---
title: 查看测试证书
description: 查看测试证书
ms.assetid: bdfa8970-fdba-4d65-8a9c-960e5f6844d6
keywords:
- 驱动程序签名 WDK、 查看测试证书
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b0e6dbfefe8d6188f0714848fbfd41f304531ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541495"
---
# <a name="viewing-test-certificates"></a>查看测试证书


创建证书并将副本放入的证书存储区后，Microsoft 管理控制台 (MMC) 证书管理单元中可以用于查看它。 执行以下操作来查看证书通过 MMC**证书**管理单元中：

1.  单击**启动**，然后单击开始搜索。

2.  若要启动证书管理单元中，键入 Certmgr.msc 并按**Enter**密钥。

3.  在证书管理单元的左窗格中，展开 PrivateCertStore 证书存储文件夹并双击证书。

以下屏幕截图显示的单元查看证书**PrivateCertStore**证书存储文件夹。

![显示测试证书的证书存储区的屏幕截图 ](images/certstore.png)

若要查看有关 Contoso.com(Test) 证书的详细信息，请双击右侧窗格中的证书。 下面的屏幕截图显示了有关证书的详细信息。

![证书窗口显示的 contoso.com 的详细信息的屏幕截图 （测试） 证书](images/certinfo.png)

请注意，证书对话框，指出："此 CA 根证书不受信任。 若要启用信任，请安装此证书受信任的根证书颁发机构存储区中。" 这是预期的行为。 因为 Windows 不信任颁发机构"Contoso.com(Test)"默认情况下，无法验证证书。

 

 





