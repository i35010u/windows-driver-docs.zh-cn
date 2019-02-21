---
title: WHQL 测试签名程序
description: WHQL 测试签名程序
ms.assetid: 241a8cfe-c7c4-4c88-9d61-831f18f4eb21
keywords:
- 驱动程序签名 WDK，WHQL 数字签名
- 签名的驱动程序 WDK、 WHQL 数字签名
- 数字签名 WDK WHQL
- 签名 WDK WHQL
- 测试签名驱动程序 WDK，WHQL 数字签名
- WHQL 数字签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1d101a5a93cab22c4077b3c68e92ba8a011ca4a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524453"
---
# <a name="whql-test-signature-program"></a>WHQL 测试签名程序


Windows 硬件质量实验室 (WHQL) 测试签名程序支持的驱动程序随后会提交到测试签名[WHQL 版本签名](whql-release-signature.md)。 独立硬件供应商 (Ihv) 参与此计划可以提交[驱动程序包](driver-packages.md)若要对其进行测试签名。 测试签名的签名[编录文件](catalog-files.md)WHQL 下 Microsoft 测试根颁发机构颁发的测试根证书生成。 测试签名目录文件，以及 WHQL 还提供了具有测试根证书的参与者。

用户可以从 WHQL 测试签名驱动程序包安装驱动程序之前，必须通过执行以下步骤配置测试计算机：

1.  若要正确安装 WHQL 测试证书，必须禁用用户帐户控制 (UAC)。 有关详细信息，请参阅[禁用 UAC](#disabling-uac)。

2.  WHQL 测试根证书 (*Testroot.cer*) 必须安装在测试计算机的受信任的根证书颁发机构证书存储区的本地计算机文件夹中。 有关详细信息，请参阅[安装 WHQL 测试根证书](#installing-the-whql-test-root-certificate)。

3.  [TESTSIGNING 启动配置选项](the-testsigning-boot-configuration-option.md)必须设置测试计算机上。 有关详细信息，请参阅[TESTSIGNING 启动配置选项设置](#setting-the-testsigning-boot-configuration-option)。

有关如何获取 WHQL 测试签名的信息，电子邮件<winqual@microsoft.com>并在主题行中包含"测试签名"。

### <a name="disabling-uac"></a>禁用 UAC

**请注意**  若要在测试计算机上禁用 UAC，您必须能够登录，或者提供的本地组成员的凭据**管理员**组。

 

可以通过执行以下步骤禁用 UAC 在 Windows 7 上：

1.  上**启动**菜单中，键入"UAC"，然后单击**更改用户帐户设置**。
2.  将滑动条移动到底部 (**永远不会通知**)，然后单击**确定**。

可以通过执行以下步骤禁用 UAC 在 Windows Vista 和 Windows Server 2008 上：

1.  启动控制面板并双击**用户帐户**。
2.  在用户帐户任务窗口中，单击**打开或关闭用户帐户控制**。
3.  清除**使用用户帐户控制 (UAC) 帮助保护您的计算机**复选框，然后依次**确定**。

一旦禁用 UAC，则必须重新启动测试计算机以应用更改。

### <a name="installing-the-whql-test-root-certificate"></a>安装 WHQL 测试根证书

WHQL 测试根证书是测试计算机上安装，通过执行以下步骤：

1.  双击测试根证书文件 (*Testroot.cer*)，然后单击**安装证书**。

2.  单击**将所有证书都放入下列存储**，然后单击**浏览**。

3.  选择**显示物理存储区**复选框，，然后展开**受信任的根证书颁发机构**。

4.  选择本地计算机文件夹，然后依次**确定**。

    **请注意**  如果 UAC 之前未禁用在测试计算机上，不会显示本地计算机文件夹。

     

5.  完成证书导入向导，接受所有默认设置安装证书。

### <a name="setting-the-testsigning-boot-configuration-option"></a>设置 TESTSIGNING 启动配置选项

Microsoft 测试根颁发机构时通过设置启用测试签名接受[TESTSIGNING 启动配置选项](the-testsigning-boot-configuration-option.md)测试签名驱动程序包将安装在计算机上。 通过执行以下步骤启用此选项：

1.  打开提升的命令提示符窗口。 若要打开提升的命令提示符窗口，创建到 Cmd.exe 的桌面快捷方式，右键单击 Cmd.exe 快捷方式，然后选择**以管理员身份运行**。

2.  在提升的命令提示符窗口中，运行以下命令：

    **BCDEdit /SET TESTSIGNING 上**

3.  重新启动测试计算机以应用更改。

 

 





