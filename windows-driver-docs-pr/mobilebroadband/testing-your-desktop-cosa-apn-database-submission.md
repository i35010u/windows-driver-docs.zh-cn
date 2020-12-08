---
title: 测试桌面 COSA/APN 数据库提交
description: 测试桌面 COSA/APN 数据库提交
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3431779b496e49a1586a4c7277797462a0c779
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829997"
---
# <a name="testing-your-desktop-cosaapn-database-submission"></a>测试桌面 COSA/APN 数据库提交

向 Microsoft 提交 APN 更新请求之前，o 或 MVNO 必须验证要提交的 APN 条目，这一点非常重要。 Microsoft 没有访问你的网络的权限，因此你有责任确保提交的值有效且正常工作。

## <a name="contact-your-microsoft-tam"></a>与 Microsoft TAM 联系

测试和提交接入点更新的第一步是与你的 TAM 合作，通过 Microsoft 客户服务和支持开启 MS 解决案例。 这种情况用于跟踪目的。 在完成 MS 求解案例后，请向支持工程师提供以下信息：

-   包含 APN 信息的已完成电子表格。

如果你没有 TAM：
-   ) MICROSOFT (642-7676) ，联系 Microsoft 客户服务和 800 (支持人员。
-   通知客户服务代表需要 COSA/APN 数据库更新。
-   将电子表格提供给支持工程师。
-   如有必要，请根据需要将 Windows 8 或 Windows 10 指定为产品。

> [!NOTE]
> 你将需要提供信用卡才能打开事件，但不会向你收费。 

## <a name="test-your-submission-for-desktop-cosa"></a>测试桌面 COSA 的提交

此过程适用于 Windows 10 版本1703及更高版本。

将包含 APN 信息的已完成电子表格提交到 TAM 后，Microsoft 将为你创建一个 ppkg) 文件的预配 ( 包，并将其返回给你，以便可以安装和测试你的 APN。 

有关如何安装预配包文件的详细信息，请参阅 [应用预配包](/windows/deploy/provisioning-apply-package)。

### <a name="modify-the-local-cosa-database-desktop-cosa"></a>修改本地 COSA 数据库 (desktop COSA) 

完成接入点信息电子表格并将其提交到 TAM 后，请按照以下步骤测试从 Microsoft 收到的已更新 COSA 预配包 (PPKG) 。

这些步骤需要 Microsoft 的脚本来应用并测试 PPKG 文件。 使用以下链接下载最新版本的脚本： <https://go.microsoft.com/fwlink/p/?linkid=866771> 。

#### <a name="apply-the-test-ppkg-file"></a>应用测试 PPKG 文件

> [!IMPORTANT]
> 执行以下操作之前，请先创建原始预配包的备份。 原始预配包位于以下位置： `%systemroot%\Provisioning\Cosa\Microsoft\Microsoft.Windows.Cosa.Desktop.Client.ppkg` 。

1. 从设备中删除任何 SIM （如果有）。
2. 将脚本和新的 PPKG 文件复制到本地目录。
3. 打开提升的命令提示符窗口，更改为包含脚本的目录。
4. 使用此语法运行脚本以应用 PPKG： `ApplyCosaProvisioning.BAT -a <full path to the PPKG local directory>` 。
   1. 例如：`ApplyCosaProvisioning.BAT -a "C:\FromMicrosoft\Microsoft.Windows.Cosa.Desktop.Client.ppkg"`
5. 插入 SIM 和 await 预配。

#### <a name="restore-the-original-ppkg-file"></a>还原原始 PPKG 文件

> [!WARNING]
> 验证从 Microsoft 收到的新 PPKG 后，请始终通过以下步骤还原。 还原到原始 PPKG 将确保通过 Windows 更新接收最新的 COSA 更新。

1. 验证后，从设备中删除 SIM。
2. 请运行具有以下语法的脚本以还原原始 PPKG： `ApplyCosaProvisioning.BAT -r` 。
3. 请插入 SIM 以使设置生效，并阅读原始 PPKG。

#### <a name="collect-logs-in-case-of-failure"></a>在发生故障的情况下收集日志

若要在测试过程中发生故障时收集日志，请执行以下步骤：

1. 从设备中删除任何 SIM。
2. 运行具有以下语法的脚本以启动 *netsh* 日志记录： `ApplyCosaProvisioning.BAT -l` 。
3. 插入 SIM 并等待预配失败。
4. 按照工具的提示来结束日志记录。
5. 以压缩格式将日志发送到 Microsoft。

## <a name="test-your-submission-for-the-apn-database-apndatabasexml"></a>测试对 APN 数据库的提交 ( # A0) 

在 windows 10 版本1703之前，将此过程用于 windows 8、Windows 8.1 和 windows 10 版本。

可以通过两种方式确保 APN 条目在提交到 Microsoft 之前工作：

-   [编辑当前配置文件的 APN 值](#editprofile)

-   [修改本地 APN 数据库](#modifydatabase)

### <a name="editing-apn-values-for-the-current-profile"></a><a href="" id="editprofile"></a> 编辑当前配置文件的 APN 值

测试 APN 能否连接到网络的一种简单方法是编辑当前配置文件，并将该 APN 插入到配置文件中。 若要执行此测试，请执行以下步骤：

> [!NOTE]
> 此测试不模拟完整的体验，如 [修改本地 APN 数据库](#modifydatabase) 部分中所述。 

1.  将一个 SIM 卡插入到使用你要测试的 APN 值的 PC 中。

2.  打开 PC，登录到 Windows，然后打开 "Windows 连接管理器"。 移动宽带连接应会出现。

3.  右键单击移动宽带连接，然后选择 " **查看连接属性**"。

4.  输入要测试到此对话框中的 APN 值。

5.  保存你所做的更改，然后尝试连接到移动宽带网络。

### <a name="modify-the-local-apn-database"></a><a href="" id="modifydatabase"></a>修改本地 APN 数据库

提交 APN 更新之前，应先编辑本地 APN 数据库，或创建新的 APN 数据库进行测试。 通过执行此操作，你可以密切模拟整个体验，因为 Windows 连接管理器使用的接入点选择逻辑经过了充分测试。

**修改本地 APN 连接数据库**

1. **从本地 apn 数据库文件复制任何现有值** --查看电脑上本地 apn 数据库中的现有条目，并将这些条目复制到新的 XML 文件中。 如果 APN 数据库的本地副本中没有任何 APN 条目，请跳过此步骤，并从空白 XML 文件开始。

2. **根据已发布的接入点架构修改 XML 文件中的值** –确保 apn 条目跟随 [apn 数据库架构引用](apn-schema-definition.md)。

3. **生成硬件 id** -硬件 id 指定一个或多个将 SIM 特征与数据库中的 APN 条目相匹配的硬件标识字符串。 每个字符串由 [HardwareId](hardwareid-apnxml.md) 元素指定。 建议使用 mbidgenerator.exe 来生成硬件 Id。 有关详细信息，请参阅 [使用 mbidgenerator.exe 生成硬件 id](using-mbidgeneratorexe-to-generate-hardware-ids.md)。

4. **验证生成的文件是否符合已发布的 APN 数据库架构** --始终执行架构检查以确保生成的文件符合 [APN 数据库架构引用](apn-schema-definition.md)。

5. **在电脑上用新数据库覆盖 APN 连接数据库**

   1.  在提升的命令提示符下，键入 **cd% systemroot% \\ system32** ，然后按 enter。

   2.  键入 **takeown \\ApnDatabase.xml** ，然后按 enter。

   3.  键入 **icacls .\ApnDatabase.xml/grant% username%： F** ，然后按 enter。

   4.  将您的自定义版本的 ApnDatabase.xml 文件复制到该目录。

6. 验证本地 APN 数据库中是否存在此 APN 条目：

   1. 通过运行以下命令确保不存在任何现有移动宽带配置文件： **netsh mb show** profile

   2. 如果移动宽带配置文件存在，则键入 **netsh mb profile interface = &lt; interface name &gt; name = &lt; profile &gt; name**

   3. 通过运行以下命令，确保设备没有预配的上下文： **netsh mb show provisionedcontext interface = &lt; interface name &gt;**

      **注意** 如果设备提供了预配的上下文，则 Windows 将使用该预配的上下文（而不是本地 APN 数据库）中的 APN，你将无法测试 APNs。 如果设备具有预配的上下文，则需要获取不提供预配上下文的另一台设备。    

   4. 打开 Windows 连接管理器。 它将显示范围内的 Wi-Fi 和移动宽带网络。

   5. 选择移动网络，然后单击 " **连接**"。

   6. 如果有多个 APNs 与 SIM 属性匹配，则在成功连接之前，Windows 连接管理器将尝试每个匹配的 APNs。 如果没有 APNs connect，Windows 连接管理器会显示错误或显示自定义接入点输入屏幕，允许用户输入自定义接入点。

      **注意** 在 APN 数据库中指定的自动连接顺序用于确定尝试 APNs 的顺序。         

   7. 如果 APN 数据库中只有一个 APN，Windows 将自动连接到操作员网络。

> [!NOTE]
> 通过打开 Windows 连接管理器，右键单击网络的移动宽带条目，然后单击 " **属性**"，可以查看哪些 APN 应用到了连接配置文件。 
