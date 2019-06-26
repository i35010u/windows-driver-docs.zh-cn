---
title: 用于内核模式代码签名的交叉证书
description: 此信息描述了如何获取和使用交叉证书进行代码签名用于 Microsoft Windows 内核模式二进制文件。
ms.assetid: 0A1364BF-04DA-4F1C-803A-18FE2A5EF390
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71c9b085148c7f2162052a63b3069eb8326eca30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378841"
---
# <a name="cross-certificates-for-kernel-mode-code-signing"></a>用于内核模式代码签名的交叉证书


此信息描述了如何获取和使用交叉证书进行代码签名用于 Microsoft Windows 内核模式二进制文件。

**请注意**  了解也请查阅 Microsoft 安全公告 ([2880823](https://docs.microsoft.com/security-updates/SecurityAdvisories/2016/2880823))"不推荐使用的 sha-1 哈希算法为 Microsoft 根证书计划"用于描述策略更改，其中 Microsoft将不再允许根证书颁发机构颁发 X.509 证书的 sha-1 哈希算法用于 SSL 和代码签名 2016 年 1 月 1 日之后的用途。

 

## <a name="cross-certificates-overview"></a>交叉证书概述


交叉证书是数字证书通过一个证书颁发机构 (CA) 颁发用于签署另一个证书颁发机构的根证书的公钥。 交叉证书提供一种方法创建从单个的受信任的根 CA，到多个其他 Ca 的信任链。

在 Windows 中，交叉证书：

-   允许操作系统内核有单一的受信任的 Microsoft 根颁发机构。
-   将信任链扩展到多个商业 Ca 颁发软件发布者证书 (SPCs)，用于代码签名的软件分发、 安装和在 Windows 上的装载

此处提供了交叉证书用于与 Windows Driver Kit (WDK) 代码签名工具正确签名内核模式软件。 对内核模式软件进行数字签名是类似于代码签名的任何软件的发布的 Windows。 交叉证书为数字签名的开发人员或软件发行者时添加签名的内核模式软件。 交叉证书本身是由代码签名工具添加到的数字签名的二进制文件或目录。

请参阅[Authenticode 签名的第三方 Csp](authenticode-signing-of-csps.md)详细了解如何使用交叉证书进行签名第三方加密服务提供商 (Csp)。

## <a name="selecting-the-correct-cross-certificate"></a>选择正确的交叉证书


Microsoft 提供的特定交叉证书用于代码签名的内核模式代码发出 SPCs 每个 CA。 下面的列表包含指向正确的交叉证书根颁发机构颁发您 SPC。

请按照以下步骤来识别你的 CA，，然后下载相关的交叉证书。

1.  打开 Microsoft 管理控制台 (MMC) 并添加证书管理单元中：
    1.  单击开始按钮，在搜索框中，键入"mmc"，然后按回车键。 如果出现用户帐户控制对话框，单击是。
    2.  从 MMC 文件菜单中，选择添加/删除管理单元中，...
    3.  选择证书管理单元中，并单击添加。
    4.  选择我的用户帐户，并单击完成。
    5.  再次选择证书管理单元中，然后单击添加。
    6.  选择计算机帐户，然后单击下一步。
    7.  选择本地计算机，并单击完成。

2.  在证书存储中，找到你 SPC 并双击它。 你的证书列在其中一个以下两个位置，具体取决于该证书已安装。
    -   当前用户、 个人、 证书存储区，或
    -   本地计算机个人证书存储区

3.  在中**证书**对话框中，单击**证书路径**卡，并选择证书路径中的最顶层的证书。 这是你 SPC 根颁发的 CA。
4.  通过单击查看根颁发机构证书**查看证书**按钮，然后依次**详细信息**选项卡上的新**证书**对话框。
5.  查找**颁发者**并**指纹**为此证书。 下面的列表中该 CA 的然后找到对应的条目。
6.  下载相关的交叉证书的 ca 和内核模式代码进行数字签名时使用与你 SPC 一起此交叉证书

## <a name="cross-certificate-list"></a>交叉证书列表


以下列表包含所有当前支持由 Microsoft 代码签名的内核模式代码发出 SPCs 的 Ca。

|                              CA                              |                 根证书指纹                 |                        下载链接                        |
| :----------------------------------------------------------: | :---------------------------------------------------------: | :---------------------------------------------------------: |
| Certum 受信任的网络 CA                                    | 55 43 55 15 fd d2 48 65 75 fd c5 cf 3b ad 00 第 9 频道 13 12 3d 03 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321770) |
| DigiCert 有保证的 ID 的根 CA                                  | ba 3e a5 4d 72 c1 45 d3 7c 25 5e 1e a4 0a fb c6 33 48 b9 6e | [下载](https://go.microsoft.com/fwlink/p/?linkid=321771) |
| DigiCert 全局根 CA                                      | 第 9 频道 83 39 19 f1 f3 6a 63 48 11 1e 93 02 6f d4 0e b9 6f bc 34 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321772) |
| DigiCert 高保障 EV 根 CA                           | 2f 25 13 af 39 92 db 0a 3f 79 70 9f f8 14 3b 3f 7b d2 d1 43 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321773) |
| Entrust.net 证书颁发机构 (2048)                   | 00 a3 e6 00 9e aa 73 9b 3d ee f4 b5 06 64 9 d 8a 1a 7a d3 3a | [下载](https://go.microsoft.com/fwlink/p/?linkid=321774) |
| Entrust G2 的根证书颁发机构 –                    | d8 fc 24 87 48 58 5e 17 3e fb fb 30 75 c4 b4 d6 0f 9d 8d 08 | [下载](https://go.microsoft.com/fwlink/p/?LinkId=624811) |
| GeoTrust 主证书颁发机构                     | e8 6e 80 82 99 0e 3d fa ed 81 6 d 9e b1 72 0f 91 a4 f1 a1 85 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321775) |
| GeoTrust 主证书颁发机构 – G3                | b2 bb bd fa c8 f1 a8 ad 58 95 cd 49 38 4b 22 ca 19 db 2d 1f | [下载](https://go.microsoft.com/fwlink/p/?linkid=321776) |
| GlobalSign 根 CA                                           | 抄送 1d ee bf 6d 55 c2 第 9 频道 06 1b a1 6f 10 a0 bf a6 97 9a 4a 32 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321777) |
| Go Daddy 的根证书颁发机构 – G2                     | 84 2c 5c b3 4b 73 bb c5 ed 85 64 bd ed a7 86 96 7 d 7b 42 ef | [下载](https://go.microsoft.com/fwlink/p/?linkid=321778) |
| NetLock Arany （类金色）                                   | 89 4f 1d 28 97 aa 4c 07 4 d cd 85 c5 fc 09 ee 73 b9 51 04 d8 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321779) |
| NetLock Platina （类白金）                             | 97 dd 74 97 16 20 57 29 41 dc 80 0 c 2f d8 0a 48 07 7 d 10 b0 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321780) |
| Security Communication RootCA1                               | 41 f2 8c e5 6f d8 b9 cb 46 7f b5 03 2a 3c ae 1c dc 9d 86 48 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321781) |
| Starfield 根证书颁发机构 – G2                    | 40 c2 0a 9a 33 fa d0 36 ac bf e8 2d 6c bb ee 1b 42 9b 86 de | [下载](https://go.microsoft.com/fwlink/p/?linkid=321782) |
| StartCom 证书颁发机构                             | e6 06 9e 04 8 d ea 8d 81 7a fc 41 88 b1 是 f1 d8 88 d0 af 17 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321783) |
| TC TrustCenter 类 2 CA II                                 | 42 62 ff 7d 89 70 66 aa e7 75 80 d3 3a d2 88 03 f9 a1 1a 62 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321784) |
| Thawte 主根 CA                                       | 55 38 e9 fe c1 40 30 b7 40 15 23 49 e1 15 a1 16 5 d 29 07 4a | [下载](https://go.microsoft.com/fwlink/p/?linkid=321785) |
| Thawte 主根 CA – G3                                  | ba 57 ca 5e 78 dd 2d 1d 74 76 ae 是 e9 95 3e 39 6f d0 55 46 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321786) |
| VeriSign 类 3 公共主证书颁发机构 – G5 | 57 53 4c 抄送 33 91 4c 41 f7 0e 2c bb 21 03 a1 db 18 81 7 d 8b | [下载](https://go.microsoft.com/fwlink/p/?linkid=321787) |
| VeriSign 世界根证书颁发机构              | 9e d8 cd 56 01 f0 10 56 51 eb bb 3f 57 f0 31 82 e5 fa 7e 01 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321788) |

## <a name="new-cross-certificate-list"></a>新的交叉证书列表


以下列表包含当前支持由 Microsoft 代码签名的内核模式代码发出 SPCs 的几个新的 Ca。


|                              CA                              |                 根证书指纹                 |                        下载链接                        |
| :----------------------------------------------------------: | :---------------------------------------------------------: | :---------------------------------------------------------: |
| AddTrust 外部 CA 根                                    | a7 5a c6 57 aa 7a 4c df e5 f9 de 39 3e 69 ef ca b6 59 d2 50 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321790) |
| GoDaddy 类 2 证书颁发机构                      | d9 61 24 72 ef 0f 27 87 e2 b2 d9 e0 63 a0 6b 32 fa 5e 33 3d | [下载](https://go.microsoft.com/fwlink/p/?linkid=321791) |
| Starfield 类 2 证书颁发机构                    | f8 fc 7f 3c dd 51 76 ad d2 7c f9 7f 73 96 59 09 46 6 d 9a 22 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321792) |
| UTN-USERFirst-Object                                         | ae 1e 25 26 01 30 a3 0b 1b c2 20 29 35 65 3b e5 a7 23 是 f5 | [下载](https://go.microsoft.com/fwlink/p/?linkid=321793) |
 

 





