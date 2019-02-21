---
title: 确定一个 SPC 交叉证书
description: 确定一个 SPC 交叉证书
ms.assetid: e54c6c69-6b80-4a03-b4ff-e46d565a56d9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ab1438a4a3849dac0d38c0346b8eaee526e71c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546980"
---
# <a name="determining-an-spcs-cross-certificate"></a>确定一个 SPC 交叉证书


除了从商业证书颁发机构 (CA) 获取软件发布者证书 (SPC)，必须获取交叉证书的 Microsoft 问题。 交叉证书用于验证颁发一个 SPC 的 CA 受信任的根颁发机构。 交叉证书和一个 SPC 所需的版本签名。

交叉证书是由另一个 CA 的根证书的公钥进行签名的 CA 颁发的 X.509 证书。 交叉证书允许具有单个受信任的 Microsoft 的根颁发机构，但也提供灵活地扩展到商业 Ca 颁发 SPCs 的信任链的内核。

您可以确定哪些交叉证书所需的版本签名之前，必须首先导入个人信息交换 (。*pfx*) 文件，将软件发布者证书 (SPC) 和其专用和公共密钥存储到的个人证书存储。 有关此过程的详细信息，请参阅[证书存储区导入一个 SPC](importing-an-spc-into-a-certificate-store.md)。

一次 *.pfx*文件导入到签名的计算机上的个人存储中，执行以下操作以确定其交叉证书，可用于你 SPC 版本签名。

1.  单击**启动**，然后单击**运行**。

2.  若要启动 MMC 证书管理单元中，键入 Certmgr.msc 并按**Enter**密钥。

3.  在证书存储中找到签名证书。 证书应列在以下位置，具体取决于安装的方式之一：

    -   当前用户-&gt;个人-&gt;证书存储区
    -   本地计算机-&gt;证书存储区

4.  若要打开**证书**单击证书对话框中，双精度。

5.  在中**证书**对话框中，选择**证书路径**卡，并选择证书路径中的最顶层的证书。

    这是创作你的证书的颁发根的 CA。

6.  若要查看的根颁发机构证书，请选择**查看证书**，然后单击**详细信息**属性选项卡。

7.  查找**颁发者名称**并**指纹**此证书的颁发 ca。 在的"根颁发机构交叉证书列表"部分中找到相应的交叉证书[Microsoft 交叉证书的 Windows Vista 内核模式代码签名](https://go.microsoft.com/fwlink/p/?linkid=190544)白皮书。

8.  从"根颁发机构交叉证书列表"部分下载相关的交叉证书并进行数字签名时使用此交叉证书[驱动程序包](driver-packages.md)。

有关 SPCs 和他们管理的详细信息，请参阅[软件发布者证书 (SPC)](software-publisher-certificate.md)。

 

 





