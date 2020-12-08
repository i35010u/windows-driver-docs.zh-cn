---
title: 测试签名
description: Windows 64 位版本要求在内核模式（包括驱动程序）中运行的所有软件都必须进行数字签名才能加载。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c1ee1de26028b37d6f7708dd261efc4f36e440b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828619"
---
# <a name="test-signing"></a>测试签名

从 Windows Vista 开始，Windows 基于 x64 的版本要求在内核模式（包括驱动程序）下运行的所有软件都要进行数字签名。 最初，你可以在每次启动时使用 F8 开关 (，在 Windows 加载) 之前，暂时禁用需要驱动程序中的有效签名的加载时间强制。 但这在第一次使用后将变得枯燥乏味。 您可以将内核调试器附加到您的测试计算机上，这将在您使用正确的 BCDEdit 命令后禁用相同的加载时间强制检查。 但是，最终需要在其开发期间对驱动程序进行测试签名，并最终在将驱动程序发布给用户之前对其进行签名。

## <a name="installing-an-unsigned-driver-during-development-and-test"></a>在开发和测试期间安装未签名驱动程序

在 [开发和测试过程中安装未签名驱动程序](installing-an-unsigned-driver-during-development-and-test.md)*的摘录*：

默认情况下，仅当内核可以验证驱动程序签名时，Windows Vista 和更高版本的 windows 的64位版本才会加载内核模式驱动程序。 但是，在早期的驱动程序开发和非自动测试期间，可以禁用此默认行为。 开发人员可以使用以下机制之一来暂时禁用有效驱动程序签名的加载时间强制。 但是，若要完全自动测试即插即用 (PnP) 安装的驱动程序，则必须对该驱动程序的 [编录文件](catalog-files.md) 进行签名。 需要对驱动程序进行签名的原因是 Windows Vista 和更高版本的 Windows 将为需要系统管理员授权安装驱动程序的无符号驱动程序显示 "驱动程序签名" 对话框，这可能会阻止没有必要权限的用户安装驱动程序和使用设备。 无法在 Windows Vista 和更高版本的 Windows 上禁用此 PnP 驱动程序安装行为。

## <a name="use-the-f8-advanced-boot-option"></a>使用 "F8 高级启动" 选项

Windows Vista 和更高版本的 Windows 支持 F8 高级启动选项--"禁用驱动程序签名强制"--该选项仅对当前系统会话禁用内核模式驱动程序的加载时签名强制。 此设置不会在系统重新启动期间保持。

在重新启动过程中，将显示以下启动选项屏幕，其中提供了禁用驱动程序签名强制的选项。 此设置将允许安装未签名的驱动程序以用于测试目的。

![显示 f8 高级启动选项的屏幕截图](images/tutorialf8.png)

### <a name="attach-a-kernel-debugger-to-disable-signature-verification"></a>附加内核调试器以禁用签名验证

将活动内核调试器附加到开发或测试计算机会禁用内核模式驱动程序的加载时签名强制。 若要使用此调试配置，请将调试计算机附加到开发或测试计算机，然后通过运行以下命令在开发或测试计算机上启用内核调试：

```cpp
bcdedit -debug on
```

若要使用 BCDEdit，用户必须是系统上 Administrators 组的成员，并从提升的命令提示符运行该命令。 若要打开提升的命令提示符窗口，请创建 *Cmd.exe* 的桌面快捷方式，选择并按住 (或右键单击该快捷方式) ，然后选择 " **以管理员身份运行**"。

但请注意，在某些情况下，开发人员可能必须附加内核调试器，还需要维护加载时签名强制。 有关如何实现此目的，请参阅 [附录1：在内核调试模式下强制 Kernel-Mode 签名验证](appendix-1--enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode.md) 。

## <a name="test-sign-a-driver-package"></a>测试对驱动程序包进行签名

最好的方法是测试对驱动程序包的签名，而不是使用上述两种方法来绕过驱动程序签名强制要求。 测试签名和驱动程序安装可以在开发计算机上完成，但您可能需要使用两台计算机，一个用于开发和签名，另一个用于测试。

*从*[如何 Test-Sign 驱动程序包](how-to-test-sign-a-driver-package.md)摘录：

### <a name="signing-computer"></a>正在为计算机签名

此计算机用于对 Windows Vista 和更高版本的 Windows 的驱动程序包进行测试签名。 此计算机必须运行 Windows XP SP2 或更高版本的 Windows。 为了使用 [驱动程序签名工具](../devtest/tools-for-signing-drivers.md)，此计算机必须安装 windows Vista 和更高版本的 Windows 驱动程序工具包 (WDK) 。 这也可以是开发计算机。

### <a name="test-computer"></a>测试计算机

此计算机用于安装和测试测试签名的驱动程序包。 此计算机必须运行 Windows Vista 或更高版本的 Windows。

## <a name="test-signing-procedure"></a>测试签名过程

驱动程序包将包含驱动程序二进制文件、INF 文件、CAT 文件和任何其他必要的文件。 如果驱动程序是为多个目标处理器类型构建的，则驱动程序包可能包含 x86、AMD64、IA64 等子目录。 使用开发/签名计算机执行这些步骤。

下面的过程介绍了对驱动程序包进行签名的步骤：

1. 生成目标的驱动程序。 如果要构建适用于 Windows 8.0 或 Windows 8.1 的驱动程序，请分别使用 Visual Studio 2012 或与相应的 WDK （例如，Windows 8.0 或 8.1 WDK）一起使用 Visual Studio 2013。

    下面所述的所有命令工具都应从相应的工具/生成命令窗口 Visual Studio 2012 或 Visual Studio 2013 中使用。

   >[!NOTE]
   >适用于 Visual Studio 的命令工具位于安装目录 C： \\ Program Files (x86) \\ Microsoft Visual Studio 12.0 \\ Common7 \\ 工具 \\ 快捷方式

命令提示符的五个快捷方式中的任何一个都将具有、makecert.exe、inf2cat.exe、signtool.exe、certmgr.exe 等命令。

你可以选择最常见的 "开发人员命令提示 for VS2013"。 快捷方式可以固定到任务栏以方便访问。

>[!NOTE]
>请注意，使用 Visual Studio 时，你还可以使用 Visual Studio 2013 开发环境， (也称为 IDE) 对驱动程序包进行签名。 有关详细信息，请参阅 [附录2：用 Visual Studio 为驱动程序签名](appendix-2--signing-drivers-with-visual-studio.md) 。

2. 创建驱动程序包文件夹并复制驱动程序文件，并保留所需的任何子目录，例如 C： \\ DriverTestPackage。
3. 为驱动程序包创建一个 inf 文件。 使用 inf 文件中的 [InfVerif](../devtest/infverif.md) 工具测试 inf 文件，以便不报告错误。
4. *Excerpt from* [创建测试证书](creating-test-certificates.md)摘录：

    以下命令行示例使用 MakeCert 来完成以下任务：

   - *(测试)* 中创建名为 "Contoso.com" 的自签名测试证书。 此证书对使用者名称和证书颁发机构 (CA) 使用相同的名称。

   - 将证书的副本放入名为 *ContosoTest* 的输出文件中。

   - 将证书的副本放入名为 *PrivateCertStore* 的证书存储中。 如果将测试证书放在 *PrivateCertStore* 中，则会将其与系统上的其他证书隔离开来。

    使用以下 MakeCert 命令创建 *Contoso.com (测试)* 证书：

    ```cpp
    makecert -r -pe -ss PrivateCertStore -n CN=Contoso.com(Test) ContosoTest.cer
    ```

    其中：

   - **-R** 选项创建一个自签名证书，该证书具有相同的颁发者和使用者名称。

   - **-Pe** 选项指定可以导出与证书关联的私钥。

   - **-Ss** 选项指定包含测试证书 (*PrivateCertStore*) 的证书存储的名称。

   - **-N CN =** option 指定证书的名称，Contoso.com (Test) 。 此名称与 [**SignTool**](../devtest/signtool.md) 工具一起用于标识证书。

   - *ContosoTest* 是包含测试证书的副本的文件名，Contoso.com (测试) 。 证书文件用于将证书添加到 "受信任的根证书颁发机构" 证书存储和 "受信任的发布者" 证书存储中。

    *Excerpt from* [查看测试证书](viewing-test-certificates.md)摘录：

    创建证书并将副本放入证书存储区后，可以使用 Microsoft 管理控制台 (MMC) 证书管理单元来查看该证书。 执行以下操作以通过 MMC " **证书** " 管理单元查看证书：

    1. 若要启动 "证书" 管理单元，请运行 Certmgr.msc。

    2. 在 "证书" 管理单元的左窗格中，展开 "PrivateCertStore" 证书存储文件夹，然后双击 "证书"。

    以下屏幕截图显示了 **PrivateCertStore** 证书存储文件夹的 "证书" 管理单元视图。

    ![显示测试证书的证书存储的屏幕截图 ](images/tutorialprivatecertstore.png)

    若要查看有关 Contoso.com (测试) 证书的详细信息，请在右窗格中双击该证书。 以下屏幕截图显示了有关证书的详细信息。

    !["证书" 窗口的屏幕截图，显示有关 contoso.com 的常规信息 (测试) 证书](images/tutorialcertificategeneraltab.png)

    请注意，"证书" 对话框状态： "此 CA 根证书不受信任。 若要启用信任，请在受信任的根证书颁发机构存储中安装此证书。 " 这是预期的行为。 无法验证证书，因为 Windows 不信任证书颁发机构，默认情况下，"Contoso.com (Test) "。

5. )  ( 创建编录文件。 使用如下所示的 inf2cat 工具来创建目录文件。 请注意，开关不允许有空格，/driver： &lt; 没有空间 &gt; &lt; 完整路径 &gt; ，/os：： &lt; no space &gt; &lt; os1 name &gt; ，： &lt; no space &gt; &lt; os2 name &gt; 。

    ```cpp
    inf2cat  /v  /driver:C:\DriverTestPackage  /os:7_64,7_x86 ,XP_X86
    ```

    这将创建一个目录文件，其中包含驱动程序的 .inf 文件中提供的名称。 可以有选择性地添加或全部以逗号分隔的操作系统，如下所示，不含空格。

    ```cpp
    /os:2000,XP_X86,XP_X64,Server2003_X64,Vista_X64,Vista_X86,7_x86,7_64,Server2008_x86,Server2008_x64,Sever2008_IA64,Server2008R2_x86,Server2008R2_x64,Server2008R2_IA64,8_x86,8_x64, 8_ARM, Server8_x64
    ```

    新 8.1 WDK 中更新的 inf2cat 的/os 选项值为6_3_X86、6_3_X64、6_3_ARM 和 SERVER_6_3_X64。

    版本部分的 INF 文件示例。

    ```cpp
    [Version]
    Signature="$WINDOWS NT$"
    Class=TOASTER
    ClassGuid={B85B7C50-6A01-11d2-B841-00C04FAD5171}
    Provider=%ToastRUs%
    DriverVer=09/21/2006,6.0.5736.1
    CatalogFile.NTx86  = tostx86.cat
    CatalogFile.NTIA64 = tostia64.cat
    CatalogFile.NTAMD64 = tstamd64.cat
    ```

    /Driver (或/drv) 选项指定包含一个或多个 INF 文件的目录。 在此目录中，将为包含一个或多个 CatalogFile 指令的 INF 文件创建目录文件。 目录文件的名称不能超过8.3。

    如果使用命令行参数/os：7_X64，则 Inf2Cat 将创建目录文件 tstamd64.cat。 同样，如果使用/os： XP_X86，则该工具将创建目录文件 toastx86.cat，与 Server2008R2_IA64 类似。 如果只需要一个编录文件，则 INF 文件中只有一个条目，如下所示。

    ```cpp
    CatalogFile.NT  = toaster.cat
    ```

    或者，

    ```cpp
    CatalogFile = toaster.cat
    ```

    如果 INF 文件中的日期不大于 OS 发布日期，则 inf2cat 工具将报告以下错误，前提是在 INF 文件中的/os 参数是用于 Windows 7 和日期集之前的日期。

    ```cpp
    Signability test failed.
    Errors:
    22.9.7: DriverVer set to incorrect date (must be postdated to 4/21/2009 for newest OS) in \toaster.inf
    ```

    Inf2cat 工具非常严格，它检查每个文件夹和子文件夹中是否存在具有 INF 文件中的条目的每个文件。 对于这类缺失条目，会出现有意义的错误消息。

    通过双击或右键单击该文件并选择 "打开"，可以从资源管理器打开该 cat 文件。 "安全" 选项卡将显示具有 GUID 值的一些条目。 选择 GUID 值将显示详细信息，包括驱动程序包的驱动程序文件和添加的操作系统，如下所示：

    ```cpp
    OSAttr  2:5.1,6.1
    ```

    Number 5.1 是适用于 Windows 7.0 OS 的 XP 操作系统和6.1 版本的版本号。

    建议检查 cat 文件以验证是否包含驱动程序文件和所选操作系统。 如果添加或删除了任何驱动程序文件，则已修改 INF 文件，必须重新创建并重新签名该 cat 文件。 此处的任何省略都将导致安装错误，这些错误将报告在 Vista 和更高版本上的安装日志文件 (setupapi.log 或 XP) 的 setupapi.log 文件中。

6. 针对 [驱动程序包的目录文件的测试签名](test-signing-a-driver-package-s-catalog-file.md)*摘录*：

    以下命令行说明了如何运行 SignTool 来执行以下操作：

   - 对 *toastpkg.inf* 示例 [驱动程序包](driver-packages.md)的 *tstamd64.cat* 目录文件进行测试签名。 有关如何创建此 [目录文件](catalog-files.md) 的详细信息，请参阅 [为 Test-Signing 驱动程序包创建编录文件](creating-a-catalog-file-for-test-signing-a-driver-package.md)。

   - 使用 Contoso.com (测试 PrivateCertStore 中的) 证书来测试签名。 有关如何创建此证书的详细信息，请参阅 [创建测试证书](creating-test-certificates.md)。

   - 通过时间戳颁发机构 (TSA) 来标记数字签名。

    若要对 *tstamd64.cat* 目录文件进行测试签名，请运行以下命令行：

    ```cpp
    Signtool sign /v /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.digicert.com tstamd64.cat
    ```

    其中：

   - **Sign** 命令将 SignTool 配置为对指定的编录文件 tstamd64.cat 进行签名。

   - **/V** 选项启用详细操作，其中，SignTool 显示成功执行和警告消息。

   - **/S** 选项指定包含测试证书的证书存储 (*PrivateCertStore)* 的名称。

   - **/N** 选项指定在指定的证书存储中安装的 (*Contoso.com (测试) # B3* 的证书的名称。

   - **/T** 选项指定了 `http://timestamp.digicert.com` 用于对数字签名进行时间戳的 TSA () 的 URL。

   >[!IMPORTANT]
   >包含时间戳会提供密钥吊销所需的信息，以防签名者的代码签名私钥泄漏。

- *tstamd64.cat* 指定将进行数字签名的目录文件的名称。

tstamd64.cat 指定将进行数字签名的目录文件的名称。 如前面所述，你可以打开 cat 文件

7. *修改后的摘录*： [通过嵌入的签名对驱动程序进行测试签名](test-signing-a-driver-through-an-embedded-signature.md)：

    -   在 Windows Vista 和更高版本的 windows 的64位版本中，内核模式代码签名要求表明 *启动启动驱动程序* 必须具有嵌入签名。 无论驱动程序的驱动程序包是否有经过数字签名的目录文件，此项都是必需的。

    下面是用于嵌入对内核模式驱动程序二进制文件进行嵌入的命令。

    ```cpp
    signtool sign  /v  /s  PrivateCertStore  /n  Contoso.com(Test)  /t http://timestamp.digicert.com   amd64\toaster.sys
    ```

    amd64 \\toaster.sys 指定将嵌入签名的内核模式二进制文件的名称。

    在 WDK 7.1 安装目录中，toaster 示例位于 src \\ general \\ toaster \\ toastpkg.inf \\ toastcd \\ 目录中。 Windows 8 或 8.1 WDK 示例将从 Microsoft 下载站点下载。 这些示例不附带 Windows 8 或 8.1 Windows 驱动程序工具包。

    通过在 Windows 资源管理器中双击文件打开目录文件时，将看到以下屏幕截图。 请注意，"查看签名" 现在已突出显示。

    ![显示安全目录文件的常规信息的屏幕截图](images/tutorialsecuritycatalogfilegeneraltab.png)

    如果选择 "查看签名"，则会看到下面的屏幕截图，其中提供了 "查看证书" 的下一个查看选项，该选项将从对话框本身提供 "安装证书" 选项。 下面，我们将提供使用 certmgr.exe 工具安装证书的首选命令行选项。

    ![屏幕截图显示有关数字签名的详细信息的一般信息](images/tutorialdriversignaturedetails.png)

    ![显示有关证书一般信息的屏幕截图](images/tutorialcertificategeneraltab.png)

现在可以在签名计算机或测试计算机上测试该驱动程序。 如果你使用的是测试计算机，请将驱动程序包复制到计算机，使文件结构保持不变。 还必须将该工具 certmgr.exe 复制到测试计算机。 使用测试计算机时，将测试签名 Toastpkg.inf 驱动程序包复制到 c： \\ toaster 临时文件夹。

以下过程描述了在任一计算机上用于测试驱动程序的步骤：

1. 在提升的命令窗口中运行以下命令：

    ```cpp
    bcdedit  /set  testsigning  on
    ```

    重新启动计算机。

2. [使用 certmgr.msc 在测试计算机上安装测试证书](using-certmgr-to-install-test-certificates-on-a-test-computer.md)*所选的摘录*：

    将证书 (*.cer*) 文件（用于对驱动程序进行 [测试签名](test-signing-driver-packages.md) ）复制到测试计算机。 可以将证书文件复制到测试计算机上的任何目录中。

    以下 Certmgr.msc 命令将证书文件 *CertificateFileName* 中的证书添加到测试计算机上受信任的根证书颁发机构证书存储：

    ```cpp
    CertMgr.exe /add CertificateFileName.cer /s /r localMachine root
    ```

    以下 Certmgr.msc 命令将证书文件 *CertificateFileName* 中的证书添加到测试计算机上的 "受信任的发行者" 证书存储：

    ```cpp
    CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
    ```

    其中 (*从* [**certmgr.msc**](../devtest/certmgr.md)) 摘录：

    /add CertificateName

    将指定证书文件中的证书添加到证书存储区。

    /s

    指定证书存储是系统存储区。

    /r RegistryLocation

    指定系统存储的注册表位置位于 HKEY_LOCAL_MACHINE。

    CertificateStore

    指定证书存储区（trustedpublisher），类似于 "localMachine root"。

    重新启动计算机。 你现在可以运行 Certmgr.msc，并验证 ContosoTest 在上述两个位置是否可见。 如果不可见，则安装证书的另一种方法是打开证书，并将其安装在上述两个节点上，并再次验证。

3. 验证 cat 文件和 sys 文件的签名。 打开提升的命令窗口，假定计算机中提供了 signtool.exe，请访问 cat、inf 和 sys 文件所在的驱动程序包目录。 在相应的目录中执行以下命令

    [验证编录文件的 SPC 签名](verifying-the-spc-signature-of-a-catalog-file.md)：

    ```cpp
    signtool  verify  /v  /kp  /c  tstamd64.cat  toaster.inf
    ```

    若要检查 embed 符号，请执行以下命令。

    [验证 Release-Signed 驱动程序文件的签名](verifying-the-signature-of-a-release-signed-driver-file.md)：

    ```cpp
    signtool  verify  /v  /kp  toaster.sys
    ```

    上面的两个命令会生成一个错误，因为已对其进行测试，而证书不是受信任的证书。

    ```cpp
    SignTool Error: A certificate chain processed, but terminated in a root certificate which is not trusted by the trust provider.
    ```

    在发布签名中，上述两个验证命令将非常有用，稍后将对此进行讨论。

    现在，驱动程序已准备好在测试计算机中进行安装和测试。 始终建议正确设置以下注册表项，以便在安装过程中) Windows Vista 和更高版本的操作系统 (中收集详细日志。

    ```cpp
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Setup\Loglevel=0x4800FFFF
    ```

    在% SystemRoot% \\ inf 文件中，重命名 setupapi.log 文件，然后再安装驱动程序。 安装后，将创建一个新的 log setupapi.log 文件，该文件将包含在安装过程中遇到的宝贵信息。

    成功安装驱动程序后，可以在开发计算机上或测试计算机上对其进行测试。

## <a name="installing-uninstalling-and-loading-the-test-signed-driver-package"></a>安装、卸载和加载 Test-Signed 驱动程序包

在步骤2中重新启动系统后，可以安装并加载测试签名的驱动程序包。 安装驱动程序包的方法有四种：

1. 使用 Dpinst ( # A0) 工具，它是一个用于安装驱动程序的 WDK 命令行工具，可再分发。
2. 使用 Devcon ( # A0) 工具，它是用于安装驱动程序的 WDK 命令行工具，但不可再发行。 WDK 中提供了 Devcon 工具的示例代码。 若要重新分发，可以从示例代码实现自己的 Devcon 工具，然后重新发布该工具的版本。
3. 使用 OS 提供的 Pnputil ( # A0) 工具。
4. 使用 "Windows 添加硬件向导"。

Dpinst 和 Pnputil 预安装驱动程序包，而在 Devcon 和 Windows 添加硬件向导中，还可以安装驱动程序和设备。 在设备连接到计算机时，预安装驱动程序有助于操作系统查找驱动程序。

### <a name="to-install-and-uninstall-the-driver-package-by-using-dpinst"></a>使用 DPInst 安装 (并卸载驱动程序包) 

1. 打开提升的命令窗口，并将默认目录设置为 c： \\ toaster。
2. 在 WDK 再发行目录中提供了 Dpinst.exe x86 版本、amd64 版本和 ia64 版本。 将相关版本复制到 c： \\ toaster 目录，并运行以下命令。

    ```cpp
    dpinst.exe  /PATH  c:\toaster
    ```

    上述命令将安装所有 inf 文件对应的所有驱动程序。 你还可以使用 "." 不包含当前目录中的引号。 "dpinst.exe/？" 显示此工具的所有开关。

    驱动程序 inf 文件上的/U 开关将从 DriverStore 的 FileRepository (% SystemRoot% System32 DriverStore FileRepository) 目录中删除驱动程序包，前提是已 \\ \\ \\ 删除与该驱动程序关联的设备。 借助 Dpinst 工具，只需引用驱动程序的 inf 文件即可删除驱动程序。

    ```cpp
    dpinst.exe  /U  toaster.inf
    ```

### <a name="to-install-the-driver-package-by-using-devcon"></a>使用 DevCon 安装驱动程序包

1. 打开提升的命令窗口，并将默认目录设置为 c： \\ toaster。
2. 在 WDK 工具目录中提供了 Devcon.exe x86 版本、amd64 版本和 ia64 版本。 将相关版本复制到 c： \\ toaster 目录，并运行以下命令。 此命令将安装驱动程序和设备。

    ```cpp
    devcon.exe  install <inf> <hwid>
    ```

    建议在 hwid 上使用引号 &lt; &gt; 。 对于 toaster 示例，它将为：

    ```cpp
    devcon.exe  install  c:\toaster\toaster.inf  “{b85b7c50-6a01-11d2-b841-00c04fad5171}\MsToaster”
    ```

    可以使用 "删除" 开关来删除设备。 "devcon.exe/？" 显示此工具的所有开关。 若要获取特定信息，应按如下所示为 "删除" 开关添加有关使用开关 "帮助" 的信息。

    ```cpp
    devcon.exe help remove
    ```

    以上命令提供了以下信息。

    删除具有指定硬件或实例 ID 的设备。 仅在本地计算机上有效。  (在需要时重启，请包含-r。 ) 

    ```cpp
    devcon [-r] remove <id> [<id>...]
    devcon [-r] remove =<class> [<id>...]
    <class>      Specifies a device setup class.
    Examples of <id>:
     *              - All devices
     ISAPNP\PNP0501 - Hardware ID
     *PNP*          - Hardware ID with wildcards  (* matches anything)
     @ISAPNP\*\*    - Instance ID with wildcards  (@ prefixes instance ID)
     '*PNP0501      - Hardware ID with apostrophe (' prefixes literal match - matches exactly as typed, including the asterisk.)
    ```

    删除设备后，若要删除驱动程序，需要两个命令。 使用带有 "dp_enum" 开关的第一个命令查找与计算机中安装的驱动程序包相对应的驱动程序 inf 文件名。

    ```cpp
    devcon  dp_enum
    ```

    此命令将显示与驱动程序包对应的所有 oemNnn 文件的列表，其中 Nnn 是包含类信息的十进制数，提供如下所示的信息。

    ```cpp
    oem39.inf
        Provider: Intel
        Class: Network adapters
    oem4.inf
        Provider: Dell
        Class: ControlVault Device
    ```

    若要从 DriverStore 中删除相应的驱动程序包，请使用下面显示的适用于 Intel "网络适配器" 驱动程序的以下命令：

    ```cpp
    devcon.exe dp_delete oem39.inf
    ```

### <a name="to-install-the-driver-package-by-using-pnputil"></a>使用 PnpUtil 安装驱动程序包

1. 打开提升的命令窗口，并将默认目录设置为 c： \\ toaster。
2. 运行以下命令，该命令将显示所有可用的开关。 开关的使用一目了然，无需显示任何示例。

   ```cpp
   C:\Windows\System32\pnputil.exe /?

    Microsoft PnP Utility
    Usage:
    ------
    pnputil.exe [-f | -i] [ -? | -a | -d | -e ] <INF name>
    Examples:
    pnputil.exe -a a:\usbcam\USBCAM.INF      -> Add package specified by USBCAM.INF
    pnputil.exe -a c:\drivers\*.inf          -> Add all packages in c:\drivers\
    pnputil.exe -i -a a:\usbcam\USBCAM.INF   -> Add and install driver package
    pnputil.exe -e                           -> Enumerate all 3rd party packages
    pnputil.exe -d oem0.inf                  -> Delete package oem0.inf
    pnputil.exe -f -d oem0.inf               -> Force delete package oem0.inf
    pnputil.exe -?                           -> This usage screen
    ```

### <a name="to-install-the-driver-package-by-using-the-add-hardware-wizard"></a>使用 "添加硬件向导" 安装驱动程序包

1. 打开提升的命令窗口
2. 运行 hdwwiz.cpl 以启动添加硬件向导，然后选择 "下一步" 以前往第二页
3. 选择 "高级" 选项并选择 "下一步"
4. 从列表框中选择 "显示所有设备"，然后选择 "下一步"
5. 选择 "具有磁盘" 选项
6. 输入包含 C： \\ toaster 驱动程序包的文件夹的路径
7. 选择 inf 文件，然后选择 "打开"。
8. 选择“确定”
9. 在接下来的两页中选择 "下一步"，然后选择 "完成" 以完成安装

### <a name="verify-that-the-test-signed-driver-is-operating-correctly"></a>验证 Test-Signed 驱动程序是否正常运行

若要验证 Toastpkg.inf 是否正常运行：

1. 开始设备管理器
2. 从设备列表中选择 "Toaster"。 有关示例，请参阅下面的屏幕截图。

    ![在设备管理器中显示 toaster 设备的屏幕截图](images/tutorialtoasterpackageindevicemgr.png)

3. 若要打开驱动程序的 "属性" 对话框，请双击 "Toaster Package Sample Toaster" 并选择 "属性"
4. 若要确认 Toaster 是否正常工作，请在 "常规" 选项卡上选中 "设备状态" 框

设备管理器可用于从 "属性" 对话框中卸载设备和驱动程序。

### <a name="how-to-troubleshoot-test-signed-drivers"></a>如何排查 Test-Signed 驱动程序问题

如果遇到这些过程的任何困难，请参阅 [驱动程序签名安装疑难解答](troubleshooting-driver-signing-installation.md) 。
