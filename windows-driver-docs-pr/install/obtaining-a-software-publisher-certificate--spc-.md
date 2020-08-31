---
title: 获取软件发行者证书 (SPC)
description: 获取软件发行者证书 (SPC)
ms.assetid: 50546234-e98d-40ed-b9c6-7d78cf0419ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bac0efea6b3b7ce526e31f2927a1867b36b9d880
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89094993"
---
# <a name="obtaining-a-software-publisher-certificate-spc"></a>获取软件发行者证书 (SPC)


版本签名要求：

-   软件发行者证书 (SPC) ，以及证书的公钥和私钥。

-   一个关联的交叉证书。

SPC 是通过商业证书颁发机构 (CA) 获取的。 CA 还将提供证书的私钥和公钥。 为了用于创建数字签名，SPC 和密钥必须转换为个人信息交换 (*.pfx*) 文件。 有关此过程的详细信息，请参阅 [个人信息交换 ( .pfx) 文件](personal-information-exchange---pfx--files.md)。

SPC 和密钥存储在 *.pfx* 文件中后，必须将其导入到签名计算机上的 "个人" 证书存储中。 有关详细信息，请参阅 [将 SPC 导入到证书存储中](importing-an-spc-into-a-certificate-store.md)。

Microsoft 为 Ca 颁发了每个公钥根证书的一个交叉证书，该证书支持使用软件发行者证书进行内核模式代码签名。 对驱动程序包进行发布签名时，必须使用正确的交叉证书。 若要确定发布签名所需的交叉证书，请参阅 [确定 SPC 的交叉证书](determining-an-spc-s-cross-certificate.md)。

有关提供 SPCs 的证书颁发机构的列表，以及有关交叉证书的详细信息，请参阅用于 [内核模式代码签名的交叉证书](./cross-certificates-for-kernel-mode-code-signing.md)。 按照 CA 网站上的说明获取并安装 SPC，并在签名计算机上安装相应的交叉证书。

有关 SPCs 及其管理的详细信息，请参阅 [软件发行者证书 (SPC) ](software-publisher-certificate.md)。

 

