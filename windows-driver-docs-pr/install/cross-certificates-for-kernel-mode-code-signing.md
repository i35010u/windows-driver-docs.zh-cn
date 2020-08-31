---
title: 用于内核模式代码签名的交叉证书
description: 此信息介绍如何获取和使用 Microsoft Windows 的代码签名内核模式二进制文件的交叉证书。
ms.assetid: 0A1364BF-04DA-4F1C-803A-18FE2A5EF390
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d4743a90bf287af3c360900ee573095c30ecf17
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056955"
---
# <a name="cross-certificates-for-kernel-mode-code-signing"></a>用于内核模式代码签名的交叉证书


此信息介绍如何获取和使用 Microsoft Windows 的代码签名内核模式二进制文件的交叉证书。

> [!NOTE]
> 请查看 Microsoft 安全公告 ([2880823](https://docs.microsoft.com/security-updates/SecurityAdvisories/2016/2880823)) "弃用适用于 Microsoft 根证书计划的 Sha-1 哈希算法"，其中描述了在年1月 1 2016 日之后，Microsoft 将不再允许根证书颁发机构使用 sha-1 哈希算法颁发 x.509 证书的策略更改。

> [!NOTE]
> [Microsoft 受信任的根程序](https://docs.microsoft.com/security/trusted-root/program-requirements)不再支持具有内核模式签名功能的根证书。 有关详细信息，请参阅 [弃用软件发行者证书、商业发布证书和商业测试证书](deprecation-of-software-publisher-certificates-and-commercial-release-certificates.md)。

## <a name="cross-certificates-overview"></a>交叉证书概述


交叉证书是由一个证书颁发机构颁发的数字证书 (CA) 用于对另一个证书颁发机构的根证书的公钥进行签名。 跨证书提供了一种方法，用于创建从一个受信任的根 CA 到多个其他 Ca 的信任链。

在 Windows 中，交叉证书：

-   允许操作系统内核具有单个受信任的 Microsoft 根证书颁发机构。
-   向颁发软件发行者证书的多个商业 Ca 扩展信任链 (SPCs) ，用于在 Windows 上分发、安装和加载代码签名软件

此处提供的交叉证书适用于 Windows 驱动程序工具包 (WDK) 代码签名工具，用于对内核模式软件进行正确的签名。 对内核模式软件进行数字签名类似于对 Windows 发布的任何软件进行代码签名。 在对内核模式软件进行签名时，开发人员或软件发行者会将交叉证书添加到数字签名。 代码签名工具将跨证书本身添加到二进制文件或目录的数字签名。

有关如何使用交叉证书对第三方加密服务提供程序进行签名的详细信息，请参阅 [第三方 csp 的 Authenticode 签名](authenticode-signing-of-csps.md) (csp) 。

## <a name="selecting-the-correct-cross-certificate"></a>选择正确的交叉证书


Microsoft 为每个 CA 提供了一个特定的交叉证书，用于为代码签名内核模式代码颁发 SPCs。 下面的列表包含一个链接，该链接指向颁发 SPC 的根颁发机构的正确交叉证书。

按照以下步骤标识 CA，然后下载相关的交叉证书。

1.  打开 Microsoft 管理控制台 (MMC) 并添加 "证书" 管理单元：
    1.  选择 "开始" 按钮，在搜索框中键入 "mmc"，然后从搜索结果中选择 "mmc"。 如果出现 "用户帐户控制" 对话框，请选择 "是"。
    2.  从 MMC 的 "文件" 菜单中，选择 "添加/删除管理单元 ..."
    3.  选择 "证书" 管理单元，然后选择 "添加"。
    4.  选择 "我的用户帐户"，然后选择 "完成"。
    5.  再次选择 "证书" 管理单元，然后选择 "添加"。
    6.  选择 "计算机帐户"，然后选择 "下一步"。
    7.  选择 "本地计算机"，然后选择 "完成"。

2.  在证书存储中找到 SPC，然后双击它。 证书在以下两个位置之一列出，具体取决于证书的安装方式。
    -   当前用户、个人证书存储区或
    -   本地计算机个人证书存储区

3.  在 " **证书** " 对话框中，选择 " **证书路径** " 选项卡，然后在证书路径中选择最顶层的证书。 这是适用于 SPC 的根颁发机构的 CA。
4.  选择 "**查看证书**" 按钮，然后选择 "新建**证书**" 对话框的 "**详细信息**" 选项卡，以查看根证书颁发机构证书。
5.  查找此证书的 **颁发者** 和 **指纹** 。 然后在下面的列表中找到此 CA 对应的条目。
6.  下载 CA 的相关交叉证书，并在对内核模式代码进行数字签名时，将此跨证书与 SPC 一起使用

## <a name="cross-certificate-list"></a>交叉证书列表


下面的列表包含 Microsoft 当前支持的用于为代码签名内核模式代码颁发 SPCs 的所有 Ca。

|                              CA                              |                 根证书指纹                 |到期日期|                        下载链接                        |
| :----------------------------------------------------------: | :---------------------------------------------------------: | :-----------: | :---------------------------------------------------------: |
| Certum 可信网络 CA                                    | 55 43 55 15 fd d2 48 65 75 fd c5 cf 3b ad 00 c9 13 12 3d 03 | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321770) |
| DigiCert 有保障的 ID 根 CA                                  | ba 3e a5 4d 72 c1 45 d3 7c 25 5e 1e a4 0a fb c6 33 48 b9 6e | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321771) |
| DigiCert 全局根 CA                                      | c9 83 39 19 f1 f3 6a 63 48 11 1e 93 02 6f d4 0e b9 6f bc 34 | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321772) |
| DigiCert 高保障 EV 根 CA                           | 2f 25 13 af 39 92 db 0a 3f 79 70 9f f8 14 3b 3f 7b d2 d1 43 | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321773) |
| Entrust.net 证书颁发机构 (2048)                   | 00 a3 e6 00 9e aa 73 9b 3d ee f4 b5 06 64 9d 8a 1a 7a d3 3a | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321774) |
| Entrust 根证书颁发机构– G2                    | d8 fc 24 87 48 58 5e 17 3e fb fb 30 75 c4 b4 d6 0f 9d 8 d 08 | 2025/07/07    | [下载](https://go.microsoft.com/fwlink/p/?LinkId=624811) |
| GeoTrust 主要证书颁发机构                     | e8 6e 80 82 99 0e 3d fa ed 81 6d 9e b1 72 0f 91 a4 f1 a1 85 | 2021/02/22    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321775) |
| GeoTrust 主证书颁发机构– G3                | b2 bb bd fa c8 f1 a8 ad 58 95 cd 49 38 4b 22 ca 19 db 2d 1f | 2021/02/22    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321776) |
| GlobalSign 根 CA                                           | cc 1d ee bf 6d 55 c2 c9 06 1b a1 6f 10 a0 bf a6 97 9a-z 4a 32 | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321777) |
| 中转 Daddy 根证书颁发机构– G2                     | 84 2c 5c b3 4b 73 bb c5 ed 85 64 bd ed a7 86 96 7d 7b 42 ef | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321778) |
| NetLock Arany (类金牌)                                    | 89 4f 1d 28 97 aa 4c 07 4d cd 85 c5 fc 09 ee 73 b9 51 04 d8 | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321779) |
| NetLock Platina (类白金)                              | 97 dd 74 97 16 20 57 29 41 dc 80 0c 2f d8 0a 48 07 7d 10 b0 | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321780) |
| 安全通信 RootCA1                               | 41 f2 8c e5 6f d8 b9 cb 46 7f b5 03 2a 3c ae 1c 1c 9d 86 48 | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321781) |
| Starfield 根证书颁发机构– G2                    | 40 c2 0a 9a-z 33 fa d0 36 ac bf e8 2d 6c bb ee 1b 42 9b 86 de | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321782) |
| StartCom 证书颁发机构                             | e6 06 9e 04 8 d ea 8 d 81 7a fc 41 88 b1 为 f1 d8 88 d0 af 17 | 2021/04/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321783) |
| TC TrustCenter Class 2 CA II                                 | 42 62 ff 7d 89 70 66 aa e7 75 80 d3 3a d2 88 03 f9 a1 1a 62 | 2021/04/11    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321784) |
| Thawte 主要根 CA                                       | 55 38 e9 fe c1 40 30 b7 40 15 23 49 e1 15 a1 16 5d 29 07 4a | 2021/02/22    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321785) |
| Thawte 主根 CA-G3                                  | ba 57 ca 5e 78 dd 2d 1d 74 76 ae e9 95 3e 39 6f d0 55 46 | 2021/02/22    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321786) |
| VeriSign Class 3 公共主证书颁发机构-G5 | 57 53 4c cc 33 91 4c 41 f7 0e 2c bb 21 03 a1 db 18 81 7d 8b | 2021/02/22    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321787) |
| VeriSign 通用根证书颁发机构              | 9e d8 cd 56 01 f0 10 56 51 eb bb 3f 57 f0 31 82 e5 fa 7e 01 | 2021/02/22    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321788) |

## <a name="new-cross-certificate-list"></a>新建交叉证书列表


下面的列表包含 Microsoft 当前支持的用于为代码签名内核模式代码颁发 SPCs 的多个新 Ca。


|                              CA                              |                 根证书指纹                 |到期日期|                         下载链接                        |
| :----------------------------------------------------------: | :---------------------------------------------------------: | :-----------: | :---------------------------------------------------------: |
| AddTrust 外部 CA 根                                    | a7 5a c6 57 aa 7a 4c df e5 f9 de 39 3e 69 ef ca b6 59 d2 50 | 2023/08/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321790) |
| GoDaddy 2 类证书颁发机构                      | d9 61 24 72 ef 0f 27 87 e2 b2 d9 e0 63 a0 6b 32 fa 5e 33 3d | 2023/08/27    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321791) |
| Starfield 2 类证书颁发机构                    | f8 fc 7f 3c dd 51 76 ad d2 7c f9 7f 73 96 59 09 46 6d 9a-z 22 | 2023/08/27    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321792) |
| UTN-USERFirst-Object                                         | ae 1e 25 26 01 30 a3 0b 1b c2 20 29 35 65 3b e5 a7 23 | 2023/08/15    | [下载](https://go.microsoft.com/fwlink/p/?linkid=321793) |
 

 





