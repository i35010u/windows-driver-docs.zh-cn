---
title: 验证码数字签名
description: 验证码数字签名
ms.assetid: b4cddf64-dc1a-47b7-803d-afb1e175c9d5
keywords:
- 验证码 WDK 驱动程序签名
- 驱动程序签名 WDK，验证码
- 签署驱动程序 WDK，验证码
- 数字签名 WDK，验证码
- 签名 WDK，验证码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40529ece337b1b32c1b3107204b933f3bb2f0eb1
ms.sourcegitcommit: ba351c01be491b8ab5c74d778ab02c8766a5667a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "67041374"
---
# <a name="authenticode-digital-signatures"></a>验证码数字签名


验证码是标识的验证码签名软件发布者的 Microsoft 代码签名技术。 此外将验证码验证的软件具有未被篡改由于签名和发布。

验证码使用加密技术来验证发布服务器标识和代码完整性。 它结合了数字签名，受信任的实体，包括证书颁发机构 (Ca)，以确保驱动程序产生的用户从规定的发布服务器的基础结构。 验证码，用户可以通过链接到受信任的根证书的数字签名中的证书来验证软件发布者的标识。

使用验证码，软件发布者进行签名的驱动程序或[驱动程序包](driver-packages.md)，其与标记[数字证书](digital-certificates.md)的验证的发布服务器的标识，并还提供了的接收方可验证的代码完整性的代码。 证书是一组标识的软件发布服务器的数据。 只有在该颁发机构已验证软件发布者的标识后，它是由 CA 颁发。 证书数据包括发布者的公用加密密钥。 证书通常是最终引用已知 CA （如 verisign） 到此类证书链的一部分。

验证码签名不会更改驱动程序的可执行部分。 相反，它执行以下任务：

-   带有嵌入签名证书，签名过程中嵌入的驱动程序文件 nonexecution 一部分中的数字签名。 有关此过程的详细信息，请参阅[驱动程序文件中嵌入签名](embedded-signatures-in-a-driver-file.md)。

-   使用数字签名[编录文件](catalog-files.md)( *.cat*)，则签名过程需要在每个文件的内容从生成文件哈希值[驱动程序包](driver-packages.md)。 此哈希值包含在目录文件。 使用嵌入式签名然后签名的编录文件。 这样一来，目录文件是一种分离签名。

**请注意**  [硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=227016)具有不同的设备类型的测试类别。 可以在找到的测试类别列表[HLK API 参考](https://docs.microsoft.com/windows-hardware/test/hlk/api/hlk-api-reference)。 如果此列表中包含的设备类型的测试类别，应获取软件发行者[WHQL 版本签名](whql-release-signature.md)有关[驱动程序包](driver-packages.md)但是，如果 HCK 不具有适用于的测试计划设备类型的软件发布者可以通过使用 Microsoft Authenticode 技术签名驱动程序包。 有关此过程的详细信息，请参阅[公开发布的版本的签名驱动程序](signing-drivers-for-public-release.md)。

 

 

 





