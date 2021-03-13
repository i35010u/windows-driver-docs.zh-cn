---
title: 确定 SPC 的交叉证书
description: 确定 SPC 的交叉证书
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e429435a89865fed3cfb1d88164243581fe19ca
ms.sourcegitcommit: 5524e265f46836100be5fb36ca6fdcac488ab274
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2021
ms.locfileid: "103417248"
---
# <a name="determining-an-spcs-cross-certificate"></a>确定 SPC 的交叉证书


除了从商业证书颁发机构 (CA) 获取软件发行者证书 (SPC) ，你必须获取 Microsoft 颁发的交叉证书。 使用交叉证书来验证颁发 SPC 的 CA 是否为受信任的根证书颁发机构。 发布签名需要使用交叉证书和 SPC。

交叉证书是由 CA 颁发的 x.509 证书，用于对另一 CA 的根证书的公钥进行签名。 跨证书允许内核具有单个受信任的 Microsoft 根证书颁发机构，还可以灵活地将信任链扩展到颁发 SPCs 的商业 Ca。

必须首先导入个人信息交换 (，然后才能确定发布签名所需的交叉证书。*pfx*) 文件，用于将软件发行者证书 (SPC) 及其私钥和公钥存储到个人证书存储区中。 有关此过程的详细信息，请参阅 [将 SPC 导入到证书存储中](importing-an-spc-into-a-certificate-store.md)。

一旦将 *.pfx* 文件导入到签名计算机上的 "个人" 存储区中，请执行以下操作以确定可以将哪种交叉证书与 SPC 一起用于发布签名。

1.  单击 " **开始** "，然后单击 " **运行**"。

2.  若要启动 MMC 证书管理单元，请键入 Certmgr.msc，然后按 **enter** 键。

3.  在证书存储中找到签名证书。 此证书应列在下列位置之一中，具体取决于它的安装方式：

    -   当前用户- &gt; 个人 &gt; 证书存储
    -   本地计算机- &gt; 证书存储

4.  若要打开 " **证书** " 对话框，请双击该证书。

5.  在 " **证书** " 对话框中，选择 " **证书路径** " 选项卡，然后在证书路径中选择最顶层的证书。

    这是颁发证书的根证书的 CA。

6.  若要查看根证书颁发机构证书，请选择 " **查看证书**"，然后单击 " **详细信息** 属性" 选项卡。

7.  查找此证书的颁发 CA 的 **颁发者名称** 和 **指纹** 。 使用 [用于内核模式代码签名的交叉证书](./cross-certificates-for-kernel-mode-code-signing.md) 来查找相应的交叉证书。

8.  从 "根机构交叉证书列表" 部分下载相关的交叉证书，并在对 [驱动程序包](driver-packages.md)进行数字签名时使用此交叉证书。

有关 SPCs 及其管理的详细信息，请参阅 [软件发行者证书 (SPC) ](software-publisher-certificate.md)。

 

