---
title: 获取软件发行者证书 (SPC)
description: 获取软件发行者证书 (SPC)
ms.assetid: 50546234-e98d-40ed-b9c6-7d78cf0419ca
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ade47f521f61fa7f0d31afac83c52df7c9d3854
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106438"
---
# <a name="obtaining-a-software-publisher-certificate-spc"></a>获取软件发行者证书 (SPC)


版本签名需要：

-   软件发行者证书 (SPC)，以及证书的公钥和私钥的加密密钥。

-   关联的交叉证书。

通过商业证书颁发机构 (CA) 获取 SPC。 CA 还将提供的证书的专用和公共密钥。 若要使用用于创建数字签名的 SPC 和密钥必须转换为个人信息交换 (*.pfx*) 文件。 有关此过程的详细信息，请参阅[个人信息交换 (.pfx) 文件](personal-information-exchange---pfx--files.md)。

SPC 和密钥存储在后 *.pfx*文件，它们必须导入到签名的计算机上的个人证书存储。 有关详细信息，请参阅[证书存储区导入一个 SPC](importing-an-spc-into-a-certificate-store.md)。

Microsoft 发布了一个交叉证书为每个密钥的公共根证书对于支持的软件发布者证书使用的内核模式代码签名的 Ca。 版本签名的驱动程序包时，必须使用正确的交叉证书。 若要确定哪些交叉证书所需的版本签名，请参阅[确定一个 SPC 交叉证书](determining-an-spc-s-cross-certificate.md)。

提供 SPCs 的证书颁发机构的列表以及有关交叉证书的详细信息，请参阅[内核模式代码签名的交叉证书](https://docs.microsoft.com/windows-hardware/drivers/install/cross-certificates-for-kernel-mode-code-signing)。 按照用于获取 CA 的网站上的说明和安装 SPC 和对应的交叉证书签名的计算机上。

有关 SPCs 和他们管理的详细信息，请参阅[软件发布者证书 (SPC)](software-publisher-certificate.md)。

 

 





