---
title: 测试桌面 COSA/APN 数据库提交
description: 测试桌面 COSA/APN 数据库提交
ms.assetid: 8f45dbf0-4f96-4d11-b2a2-41b9e75b5e9b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44c3b835a15c6fd02855bf69f1e81344f6b6b7c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376993"
---
# <a name="testing-your-desktop-cosaapn-database-submission"></a>测试桌面 COSA/APN 数据库提交

在提交给 Microsoft 的 APN 更新请求之前, 是重要的 MNO 或 MVNO，以验证它们正准备提交 APN 条目。 Microsoft 不具有访问网络，因此它是由你负责确保要提交的值是有效且工作正常。

## <a name="contact-your-microsoft-tam"></a>联系 Microsoft 客户 TAM

测试和提交你的 APN 更新的第一步是使用与 Microsoft 客户服务和支持案例 MS 求解 TAM。 这种情况下是用于跟踪目的。 打开 MS 求解用例后，请向支持工程师提供以下信息：

-   一个已完成的电子表格，包含你的 APN 信息。

如果不具有 TAM:
-   通过调用 (800) MICROSOFT (642-7676)，请联系 Microsoft 客户服务和支持。
-   通知客户需要 COSA/APN 数据库更新的服务代表。
-   向支持工程师提供电子表格。
-   如有需要，指定为该产品，根据 Windows 8 或 Windows 10。

> [!NOTE]
> 将需要提供信用卡来打开事件，但您不会收费。 

## <a name="test-your-submission-for-desktop-cosa"></a>测试你的桌面 COSA 的提交

适用于 Windows 10，版本 1703年及更高版本使用此过程。

提交您已完成的电子表格，其中包含您的 TAM 你 APN 的信息后，Microsoft 将为你创建预配的包 (.ppkg) 文件，并将其返回到你，因此可以安装和测试你的 APN。 

有关如何安装预配包文件的详细信息，请参阅[预配包应用](https://technet.microsoft.com/itpro/windows/deploy/provisioning-apply-package)。

### <a name="modify-the-local-cosa-database-desktop-cosa"></a>修改本地 COSA 数据库 (桌面 COSA)

请按照以下步骤来测试更新 COSA 预配程序包 (PPKG) 从 Microsoft 接收完成您 APN 信息的电子表格并将其提交到您的 TAM 之后。

这些步骤需要 Microsoft 应用和测试 PPKG 文件中的脚本。 使用以下链接下载最新版本的脚本： <https://go.microsoft.com/fwlink/p/?linkid=866771>。

#### <a name="apply-the-test-ppkg-file"></a>应用测试 PPKG 文件

> [!IMPORTANT]
> 执行以下操作之前创建的备份的原始的预配包。 原始的预配包位于此处： `%systemroot%\Provisioning\Cosa\Microsoft\Microsoft.Windows.Cosa.Desktop.Client.ppkg`。

1. 如果有，请从该设备，删除任何 SIM。
2. 将该脚本，并将新的 PPKG 文件复制到本地目录。
3. 打开提升的命令提示符窗口并更改到包含该脚本的目录。
4. 使用此语法以应用 PPKG 运行脚本： `ApplyCosaProvisioning.BAT -a <full path to the PPKG local directory>`。
   1. 例如：`ApplyCosaProvisioning.BAT -a "C:\FromMicrosoft\Microsoft.Windows.Cosa.Desktop.Client.ppkg"`
5. 插入 sim 卡，然后等待预配。

#### <a name="restore-the-original-ppkg-file"></a>还原原始 PPKG 文件

> [!WARNING]
> 新 PPKG 收到过来自 Microsoft 的验证完成后，始终将其还原的以下步骤。 还原到原始 PPKG 将确保接收最新的 COSA 更新通过 Windows Update。

1. 验证后，从设备中删除 sim 卡。
2. 使用此语法以还原原始 PPKG 运行脚本： `ApplyCosaProvisioning.BAT -r`。
3. 将预配 SIM 才会生效，读取原始 PPKG。

#### <a name="collect-logs-in-case-of-failure"></a>收集故障日志

若要在测试过程中收集日志出现故障时，请执行以下步骤：

1. 从设备中删除任何 SIM。
2. 使用此语法以开始运行该脚本*netsh*日志记录： `ApplyCosaProvisioning.BAT -l`。
3. 插入 sim 卡，并等待预配失败。
4. 请按照结束日志记录工具的提示。
5. 以压缩格式向 Microsoft 发送日志。

## <a name="test-your-submission-for-the-apn-database-apndatabasexml"></a>测试你的提交对 APN 数据库 (apndatabase.xml)

Windows 8、 Windows 8.1 和 Windows 10 版本 1703年的 Windows 10 之前的版本使用此过程。

有两种方法可以确保 APN 条目工作之前将它们提交给 Microsoft:

-   [编辑当前配置文件的 APN 值](#editprofile)

-   [修改本地的 APN 数据库](#modifydatabase)

### <a href="" id="editprofile"></a> 编辑当前配置文件的 APN 值

测试 APN 可以连接到网络的简单方法是编辑当前配置文件并插入到配置文件测试此 APN。 若要执行此测试，请执行以下步骤：

> [!NOTE]
> 此测试不模拟中所述的完整体验[修改本地的 APN 数据库](#modifydatabase)部分。 

1.  Sim 卡插入的 PC 的适用于你想要测试的 APN 值。

2.  打开 PC，登录到 Windows，并打开 Windows 连接管理器。 移动宽带连接应显示。

3.  右键单击移动宽带连接，然后依次**查看连接属性**。

4.  输入要测试在此对话框的 APN 值。

5.  保存所做的更改，然后尝试连接到移动宽带网络。

### <a href="" id="modifydatabase"></a>修改本地的 APN 数据库

提交的 APN 更新之前，您应该编辑本地的 APN 数据库或创建一个新的测试。 通过执行此操作，您可以因为 Windows 连接管理器使用的 APN 选择逻辑完全测试准确地模拟到完整的体验。

**修改本地的 APN 连接数据库**

1. **从本地的 APN 数据库文件复制任何现有值**-查看您的 PC 上本地的 APN 数据库中的现有条目并将复制到新的 XML 文件的这些项。 如果没有任何 APN 条目 APN 数据库的本地副本中，跳过此步骤和空白的 XML 文件开始。

2. **根据已发布的 APN 架构的 XML 文件中修改值**– 确保 APN 条目遵循[APN 数据库架构参考](apn-database-schema-reference.md)。

3. **生成您的硬件 Id** – 硬件 Id 指定一个或多个硬件标识字符串匹配到数据库中的 APN 条目的 SIM 特征。 指定每个字符串[HardwareId](hardwareid-apnxml.md)元素。 我们建议使用 mbidgenerator.exe 生成您的硬件 Id。 有关详细信息，请参阅[mbidgenerator.exe 用于生成的硬件 Id](using-mbidgeneratorexe-to-generate-hardware-ids.md)。

4. **验证你生成的文件是否符合已发布的 APN 数据库架构**-始终执行架构检查，以确保已生成的文件符合[APN 数据库架构参考](apn-database-schema-reference.md)。

5. **使用新的数据库覆盖在 PC 上的 APN 连接数据库**

   1.  从提升的命令提示符，键入**cd %systemroot%\\system32** ，然后按 ENTER。

   2.  类型**takeown /f。\\ApnDatabase.xml** ，然后按 ENTER。

   3.  类型**icacls.\ApnDatabase.xml /grant %username%: F** ，然后按 ENTER。

   4.  将你自定义的版本的 ApnDatabase.xml 文件复制到目录。

6. 验证本地的 APN 数据库中存在的 APN 条目：

   1. 确保通过运行以下命令不存在任何现有的移动宽带配置文件： **netsh mb 显示配置文件**

   2. 如果移动宽带的配置文件存在，请键入**netsh mb 的配置文件接口 =&lt;接口名称&gt;名称 =&lt;配置文件名称&gt;**

   3. 确保设备不具有预配的上下文，通过运行以下命令： **netsh mb 显示 provisionedcontext 接口 =&lt;接口名称&gt;**

      **请注意**如果设备提供了预配的上下文中，Windows 将使用该预配的上下文中 APN 而不是本地的 APN 数据库并将不能测试你的 APNs。 如果该设备已预配的上下文，则需要获取不提供预配的上下文的另一台设备。    

   4. 打开 Windows 连接管理器。 它将显示 Wi-fi 和移动宽带网络范围内。

   5. 选择移动网络，然后单击**Connect**。

   6. 如果你有 SIM 属性匹配的多个 Apn，Windows 连接管理器将尝试每个匹配的 APNs 直到成功连接发生。 如果没有任何 APNs 连接，Windows 连接管理器将显示错误，或显示自定义 APN 输入屏幕上，允许用户输入自定义 APN。

      **请注意**APN 数据库中指定的自动连接顺序用于确定在其中尝试 APNs 的顺序。         

   7. 如果必须将只有一个 APN APN 数据库中，Windows 将自动连接到运营商网络中。

> [!NOTE]
> 您所见的 APN 已应用于通过 Windows 连接管理器中打开，右键单击您的网络，移动宽带条目，然后单击连接配置文件**属性**。 

