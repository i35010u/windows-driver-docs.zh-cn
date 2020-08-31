---
title: 验证码数字签名
description: 验证码数字签名
ms.assetid: b4cddf64-dc1a-47b7-803d-afb1e175c9d5
keywords:
- 验证码 WDK 驱动程序签名
- 驱动程序签名 WDK，Authenticode
- 对驱动程序进行签名 WDK，Authenticode
- 数字签名 WDK，Authenticode
- 签名 WDK，Authenticode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e158385e52398c8363215806dd0a3dc0fd519b9b
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095101"
---
# <a name="authenticode-digital-signatures"></a>验证码数字签名


Authenticode 是一项 Microsoft 代码签名技术，用于标识 Authenticode 签名软件的发布者。 Authenticode 还会验证软件是否在经过签名和发布后被篡改。

Authenticode 使用加密技术来验证发行者标识和代码完整性。 它将数字签名与受信任实体（包括证书颁发机构 (Ca) ）的基础结构相结合，以确保用户的驱动程序来自于所述的发布者。 Authenticode 允许用户通过将数字签名中的证书链接到受信任的根证书来验证软件发行者的身份。

使用 Authenticode，软件发行者签署驱动程序或 [驱动程序包](driver-packages.md)，使用验证发行者身份的 [数字证书](digital-certificates.md) 对其进行标记，并为代码的接收方提供验证代码完整性的能力。 证书是用于标识软件发行者的一组数据。 仅在该颁发机构验证了软件发行者的身份后，才由 CA 颁发此证书。 证书数据包括发行者的公共加密密钥。 此证书通常是此类证书链的一部分，最终引用的是众所周知的 CA （如 VeriSign）。

Authenticode 代码签名不会改变驱动程序的可执行部分。 相反，它执行以下操作：

-   使用嵌入签名，签名过程在驱动程序文件的 nonexecution 部分中嵌入数字签名。 有关此过程的详细信息，请参阅 [驱动程序文件中的嵌入签名](embedded-signatures-in-a-driver-file.md)。

-   对于经过数字签名的 [目录文件](catalog-files.md) (*类*) ，签名过程需要从 [驱动程序包](driver-packages.md)中每个文件的内容生成文件哈希值。 此哈希值包含在目录文件中。 然后，使用嵌入的签名对该目录文件进行签名。 通过这种方式，目录文件是一种分离签名。

**注意**   [硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?linkid=227016)包含各种设备类型的测试类别。 可在 [HLK API 参考](/windows-hardware/test/hlk/api/hlk-api-reference)中找到测试类别的列表。 如果此列表中包含设备类型的测试类别，则软件发行者应为[驱动程序包](driver-packages.md)获取[WHQL 版本签名](whql-release-signature.md)，但如果 HCK 没有设备类型的测试程序，则软件发布者可以使用 Microsoft Authenticode 技术对驱动程序包进行签名。 有关此过程的详细信息，请参阅 [签署公用版驱动程序](signing-drivers-for-public-release--windows-vista-and-later-.md)。

 

 

