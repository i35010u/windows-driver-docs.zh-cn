---
title: WHQL 测试签名计划
description: WHQL 测试签名计划
keywords:
- 驱动程序签名 WDK，WHQL 数字签名
- 对驱动程序进行签名 WDK，WHQL 数字签名
- 数字签名 WDK，WHQL
- 签名 WDK，WHQL
- 测试签名驱动程序 WDK，WHQL 数字签名
- WHQL 数字签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 871a17d3a7a5b104f4d391f88991dce45a7b6893
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819459"
---
# <a name="whql-test-signature-program"></a>WHQL 测试签名计划


Windows 硬件质量实验室 (WHQL) 测试签名程序支持随后将提交以获得 [WHQL 版本签名](whql-release-signature.md)的驱动程序的测试签名。 参与此计划的独立硬件供应商 (Ihv) 可以将 [驱动程序包](driver-packages.md) 提交给测试签名。 测试签名 [目录文件](catalog-files.md) 上的签名由 WHQL 在 Microsoft 测试根颁发机构下颁发的测试根证书生成。 除了测试签名目录文件，WHQL 还为参与者提供了测试根证书。

必须先按照以下步骤配置测试计算机，然后用户才能从 WHQL 测试签名驱动程序包中安装驱动程序：

1.  必须禁用用户帐户控制 (UAC) 才能正确安装 WHQL 测试证书。 有关详细信息，请参阅 [禁用 UAC](#disabling-uac)。

2.  必须在测试计算机的 "受信任的根证书颁发机构" 证书存储的 "本地计算机" 文件夹中的测试计算机上安装 () *Testroot* 的 WHQL 测试根证书。 有关详细信息，请参阅 [安装 WHQL 测试根证书](#installing-the-whql-test-root-certificate)。

3.  必须在测试计算机上设置 [TESTSIGNING Boot 配置选项](the-testsigning-boot-configuration-option.md) 。 有关详细信息，请参阅 [设置 TESTSIGNING Boot 配置选项](#setting-the-testsigning-boot-configuration-option)。

有关如何获取 WHQL 测试签名的信息，请发送电子邮件 <winqual@microsoft.com> 并在主题行中包含 "测试签名"。

### <a name="disabling-uac"></a>禁用 UAC

**注意**  若要在测试计算机上禁用 UAC，你必须能够使用登录或提供本地 **管理员** 组的成员的凭据。

 

可以通过执行以下步骤，在 Windows 7 上禁用 UAC：

1.  在 " **开始** " 菜单上，输入 "UAC"，然后选择 " **更改用户帐户设置**"。
2.  将滑动条移动到底部 (**从不通知**) ，然后选择 **"确定"**。

可以通过执行以下步骤，在 Windows Vista 和 Windows Server 2008 上禁用 UAC：

1.  启动 "控制面板"，然后双击 " **用户帐户**"。
2.  在 "用户帐户" 任务窗口中，选择 **"打开或关闭用户帐户控制**"。
3.  清除 " **使用用户帐户控制 (UAC) 以帮助保护您的计算机** " 复选框，然后选择 **"确定"**。

禁用 UAC 后，你必须重新启动测试计算机才能应用更改。

### <a name="installing-the-whql-test-root-certificate"></a>安装 WHQL 测试根证书

通过执行以下步骤，在测试计算机上安装 WHQL 测试根证书：

1.  双击 "测试根证书" (" *Testroot* ") ，然后选择 " **安装证书**"。

2.  选择 **"将所有证书放入下列存储**"，然后选择 " **浏览**"。

3.  选中 " **显示物理存储** " 复选框，然后展开 " **受信任的根证书颁发机构**"。

4.  选择本地计算机文件夹，然后选择 **"确定"**。

    **注意**  如果以前在测试计算机上未禁用 UAC，则不会显示 "本地计算机" 文件夹。

     

5.  完成证书导入向导，并接受所有默认设置以安装证书。

### <a name="setting-the-testsigning-boot-configuration-option"></a>设置 TESTSIGNING Boot 配置选项

通过在要安装测试签名的驱动程序包的计算机上设置 [TESTSIGNING Boot 配置选项](the-testsigning-boot-configuration-option.md) 来启用测试签名时，将接受 Microsoft 测试根颁发机构。 执行以下步骤即可启用此选项：

1.  打开提升的命令提示符窗口。 若要打开提升的命令提示符窗口，请创建 Cmd.exe 的桌面快捷方式，选择并按住 (或右键单击 Cmd.exe 快捷方式) ，然后选择 " **以管理员身份运行**"。

2.  在提升的命令提示符窗口中运行以下命令：

    **BCDEdit/SET TESTSIGNING ON**

3.  重新启动测试计算机以应用更改。

 

 





