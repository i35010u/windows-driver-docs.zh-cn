---
title: 测试签名
description: Windows 64 位版本要求运行在内核模式下，其中包括驱动程序，以进行数字签名，这样才能加载的所有软件。
ms.assetid: 52F309E4-9553-456B-BBD6-217318FC7222
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a76b55ed3084b756e802d834f071e57629e63b8d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339921"
---
# <a name="test-signing"></a>测试签名


从 Windows Vista 开始，基于 x64 的 Windows 版本所需的所有软件运行在内核模式下，其中包括驱动程序，以进行数字签名，这样才能加载。 最初可能使用 F8 开关 （在每个启动，Windows 加载前） 若要暂时禁用需要有效的签名驱动程序中加载时强制。 但这将变得枯燥乏味后的第几个用途。 可以将内核调试程序附加到您在使用正确的 BCDEdit 命令后，将禁用相同加载时强制执行检查的测试计算机。 但是，最终它将成为需要测试登录到您的驱动程序在其开发和最终版本登录您的驱动程序之前将其发布到用户。

## <a name="installing-an-unsigned-driver-during-development-and-test"></a>在开发和测试期间安装未签名驱动程序


*从节选*[开发和测试期间安装未签名的驱动程序](installing-an-unsigned-driver-during-development-and-test.md):

默认情况下，64 位版本的 Windows Vista 和更高版本的 Windows 将加载的内核模式驱动程序仅当内核可以验证驱动程序签名。 但是，在早期驱动程序开发期间以及非自动测试到已禁用此默认行为。 开发人员可以使用以下机制之一来暂时禁用加载时强制实施有效的驱动程序签名。 但是，若要完全自动执行测试的情况下插即用 (PnP) 安装的驱动程序[编录文件](catalog-files.md)必须签名的驱动程序。 签名驱动程序是必需的因为 Windows Vista 和更高版本的 Windows 显示驱动程序签名需要系统管理员进行授权的驱动程序安装的未签名驱动程序的对话框中，这可能会导致无需任何用户从安装驱动程序以及使用该设备的必要权限。 不能在 Windows Vista 和更高版本的 Windows 上禁用此即插即用驱动程序安装行为。

### <a name="use-the-f8-advanced-boot-option"></a>**使用 F8 高级启动选项**

Windows Vista 和更高版本的 Windows 支持的 F8 高级启动选项-"禁用强制驱动程序签名"-禁用强制内核模式驱动程序的加载时间签名仅为当前的系统会话。 在系统重启后不保留此设置。

提供此选项来禁用该驱动程序签名强制重启期间，将显示以下的启动选项屏幕。 此设置将允许安装未签名的驱动程序用于测试目的。

![显示 f8 高级启动选项的屏幕截图](images/tutorialf8.png)

### <a href="" id="attach-a-kernel-debugger-to-disable-signature-verification"></a> 附加内核调试器来禁用签名验证

将活动内核调试程序附加到开发或测试计算机禁用内核模式驱动程序的强制加载时签名。 若要使用此调试配置，将调试的计算机附加到需要开发或测试计算机，并启用内核调试上开发或通过运行以下命令测试计算机：

```cpp
bcdedit -debug on
```

若要使用 BCDEdit，用户必须是系统上的 Administrators 组的成员并从提升的命令提示符运行命令。 若要打开提升的命令提示符窗口，请创建桌面快捷方式*Cmd.exe*，右键单击该快捷方式，然后选择**以管理员身份运行**。

但是，请注意还有一些情况下开发人员可能需要附加内核调试器，但还需要维护强制加载时签名。 请参阅[附录 1:强制在内核调试模式下的内核模式签名验证](appendix-1--enforcing-kernel-mode-signature-verification-in-kernel-debugging-mode.md)有关如何实现此目的。

## <a name="test-sign-a-driver-package"></a>测试签名驱动程序包


而不是使用上述两种方法来绕过驱动程序签名强制要求，最好的方法是测试签名驱动程序包。 在开发计算机上，可以进行测试签名和驱动程序安装，但你可能想要有两台计算机，另一个用于开发和签名，以及另一个用于测试。

*从节选*[如何测试签名驱动程序包](how-to-test-sign-a-driver-package.md):

<a href="" id="signing-computer"></a>**签名的计算机**  
这是用于测试签名驱动程序包适用于 Windows Vista 和更高版本的 Windows 的计算机。 此计算机必须运行 Windows XP SP2 或更高版本的 Windows。 若要使用[驱动程序签名工具](https://msdn.microsoft.com/library/windows/hardware/ff552958)、 此计算机必须安装 Windows Vista 和更高版本的 Windows Driver Kit (WDK) 安装。 这也可以是开发计算机。

<a href="" id="test-computer"></a>**测试计算机**  
这是用于安装和测试的测试签名驱动程序包的计算机。 此计算机必须运行 Windows Vista 或更高版本的 Windows。

## <a name="test-signing-procedure"></a>测试签名的过程


驱动程序包将包含驱动程序二进制文件、 INF 文件、 CAT 文件和任何其他必要的文件。 驱动程序包可能包含子目录，就像 x86 AMD64，IA64，如果该驱动程序生成多个目标处理器类型。 执行这些步骤使用签名开发/计算机。

以下过程介绍的步骤来测试登录驱动程序包：

1.  生成目标的驱动程序。 如果你正在为 Windows 8.0 或 Windows 8.1，创建一个驱动程序，然后使用 Visual Studio 2012 或 Visual Studio 2013 与相应的 WDK，例如，Windows 8.0 或 8.1 WDK 分别安装。

    应在相应的工具/生成命令窗口 Visual Studio 2012 或 Visual Studio 2013 中使用下面所述的所有命令工具。

    **请注意**适用于 Visual Studio 的命令工具位于安装目录，c:\\Program Files (x86)\\Microsoft Visual Studio 12.0\\Common7\\工具\\快捷方式




任何的五个快捷键的命令提示符将具有，makecert.exe、 inf2cat.exe、 signtool.exe、 certmgr.exe，等等，命令。

您可以选择其中最常见，"第命令提示符的 VS2013 开发人员"。 可以将快捷方式向下固定到任务栏以便于访问。

**请注意**请注意，与 Visual Studio 中，而不是命令工具方法的驱动程序签名，你还可用于 Visual Studio 2013 开发环境 (也称为 IDE) 签署驱动程序包。 请参阅[附录 2:签署驱动程序使用 Visual Studio](appendix-2--signing-drivers-with-visual-studio.md)有关详细信息。




2.  创建驱动程序包文件夹和复制驱动程序文件，维护任何子目录，例如需要 c:\\DriverTestPackage。
3.  创建驱动程序包的 inf 文件。 请确保的 inf 文件的日期不是在 08/21/2006 适用于 Vista 和更高版本的 Windows 8.0、 Windows 8.1、 Windows 7.0 和 Windows 7.1 日期同样之前。 最好测试使用 WDK 中的 chkinf.bat 工具上的 inf 文件，以便不会报告错误的 inf 文件。 如果打印机驱动程序，然后测试与工具 chkinf.bat 和 INFGate.exe 从 WDK 的 inf 文件。
4.  *从节选*[创建测试证书](creating-test-certificates.md):

    下面的命令行示例使用 MakeCert 来完成以下任务：

    -   创建一个名为的自签名的测试证书*Contoso.com(Test)*。 此证书使用相同的名称的使用者名称和证书颁发机构 (CA)。

    -   将证书的副本放在名为输出文件*ContosoTest.cer*。

    -   将证书的副本放在名为的证书存储中*PrivateCertStore*。 将测试证书放入*PrivateCertStore*保持独立于其他可能会在系统的证书。

    使用以下 MakeCert 命令来创建*Contoso.com(Test)* 证书：

    ```cpp
    makecert -r -pe -ss PrivateCertStore -n CN=Contoso.com(Test) ContosoTest.cer
    ```

    其中：

    -   **-R**选项具有相同的颁发者和使用者名称创建一个自签名的证书。

    -   **-Pe**选项指定与证书相关联的私钥可导出。

    -   **-Ss**选项指定包含测试证书的证书存储区的名称 (*PrivateCertStore*)。

    -   **-N CN =** 选项指定的证书，Contoso.com(Test) 的名称。 此名称用于[ **SignTool** ](https://msdn.microsoft.com/library/windows/hardware/ff551778)工具找到的证书。

    -   *ContosoTest.cer*是包含测试证书，Contoso.com(Test) 的副本的文件名。 证书文件用于将证书添加到受信任的根证书颁发机构证书存储和受信任的发行者证书存储区。

    *从节选*[查看测试证书](viewing-test-certificates.md):

    创建证书并将副本放入的证书存储区后，Microsoft 管理控制台 (MMC) 证书管理单元中可以用于查看它。 执行以下操作来查看证书通过 MMC**证书**管理单元中：

    1.  单击**启动**，然后单击开始搜索。

    2.  若要启动证书管理单元中，键入 Certmgr.msc 并按**Enter**密钥。

    3.  在证书管理单元的左窗格中，展开 PrivateCertStore 证书存储文件夹并双击证书。

    以下屏幕截图显示的单元查看证书**PrivateCertStore**证书存储文件夹。

    ![显示测试证书的证书存储区的屏幕截图 ](images/tutorialprivatecertstore.png)

    若要查看有关 Contoso.com(Test) 证书的详细信息，请双击右侧窗格中的证书。 下面的屏幕截图显示了有关证书的详细信息。

    ![证书窗口显示有关 contoso.com 的常规信息的屏幕截图 （测试） 证书](images/tutorialcertificategeneraltab.png)

    请注意，证书对话框，指出："此 CA 根证书不受信任。 若要启用信任，请安装此证书受信任的根证书颁发机构存储区中。" 这是预期的行为。 因为 Windows 不信任颁发机构"Contoso.com(Test)"默认情况下，无法验证证书。

5.  创建编录文件 （扩展名为.cat）。 使用的 inf2cat 工具，如下所示创建目录文件。 请注意，不允许有空格对于开关，/driver:&lt;没有空格&gt;&lt;完整路径&gt;，/os::&lt;没有空间&gt;&lt;os1 名称&gt;，：&lt;没有空格&gt;&lt;os2 名称&gt;。

    ```cpp
    inf2cat  /v  /driver:C:\DriverTestPackage  /os:7_64,7_x86 ,XP_X86
    ```

    这将创建一个目录文件与驱动程序的.inf 文件中提供的名称。 其他以逗号分隔的操作系统可以有选择地添加或全部，如下所示，不含空格。

    ```cpp
    /os:2000,XP_X86,XP_X64,Server2003_X64,Vista_X64,Vista_X86,7_x86,7_64,Server2008_x86,Server2008_x64,Sever2008_IA64,Server2008R2_x86,Server2008R2_x64,Server2008R2_IA64,8_x86,8_x64, 8_ARM, Server8_x64
    ```

    从新 8.1 WDK 更新的 inf2cat 具有 6_3_X86、 6_3_X64、 6_3_ARM 和 SERVER_6_3_X64 /os 选项值。

    版本部分的 INF 文件的示例。

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

    /Driver （或 /drv） 选项指定的目录，其中包含一个或多个 INF 文件。 在此目录中，为那些包含一个或多个 CatalogFile 指令的 INF 文件创建目录文件。 目录文件名称不限于 8.3 名称。

    如果使用命令行参数 /os:7_X64，Inf2Cat 创建目录文件 tstamd64.cat。 同样，该工具创建目录文件 toastx86.cat 如果 /os:XP_X86，选项用于，同样 Server2008R2_IA64。 在的情况下，需要只有一个目录文件，如下所示的 INF 文件中只有一个条目就足够了。

    ```cpp
    CatalogFile.NT  = toaster.cat
    ```

    或者，

    ```cpp
    CatalogFile = toaster.cat
    ```

    如果 INF 文件中的日期不是大于操作系统发布日期，则 inf2cat 工具将报告以下错误，如果 /os 参数是适用于 Windows 7，并且在 INF 文件中设置的日期较早的日期。

    ```cpp
    Signability test failed.
    Errors:
    22.9.7: DriverVer set to incorrect date (must be postdated to 4/21/2009 for newest OS) in \toaster.inf
    ```

    Inf2cat 工具是非常严格检查每个文件夹和子文件夹有关的 INF 文件中有条目的每个文件存在。 在此类缺少的条目将是有意义的错误消息。

    通过双单击或右键单击文件并选择打开，可以从资源管理器打开 cat 文件。 安全选项卡将显示某些条目使用 GUID 值。 选择一个 GUID 值会显示详细信息，包括驱动程序包的驱动程序文件和操作系统添加如下所示：

    ```cpp
    OSAttr  2:5.1,6.1
    ```

    5.1 的数字是 XP 操作系统的版本号和 Windows 7.0 OS 的 6.1。

    最好 cat 文件会检查以验证包含的驱动程序文件和所选的操作系统。 在任何时候如果添加或删除任何驱动程序文件，INF 文件已被修改，必须重新创建 cat 文件，并将其重新签名。 此处任何省略将导致安装错误报告上的安装日志文件 （适用于 Vista 及更高版本的 setupapi.dev.log 或 XP 的 setupapi.log 文件）。

6.  *从节选*[测试签名驱动程序包的目录文件](test-signing-a-driver-package-s-catalog-file.md):

    下面的命令行显示了如何运行 SignTool 将执行以下操作：

    -   测试签名*tstamd64.cat*的编录文件*ToastPkg*示例[驱动程序包](driver-packages.md)。 详细了解如何为这[编录文件](catalog-files.md)已创建，请参见[测试签名的驱动程序包创建编录文件](creating-a-catalog-file-for-test-signing-a-driver-package.md)。

    -   将从 PrivateCertStore Contoso.com(Test) 证书用于测试签名。 有关如何创建此证书的详细信息，请参阅[创建测试证书](creating-test-certificates.md)。

    -   时间戳的时间戳颁发机构 (TSA) 通过数字签名。

    对测试签名*tstamd64.cat*目录文件，请运行以下命令行：

    ```cpp
    Signtool sign /v /s PrivateCertStore /n Contoso.com(Test) /t http://timestamp.verisign.com/scripts/timstamp.dll tstamd64.cat
    ```

    其中：

    -   **登录**命令配置指定的目录文件进行签名的 SignTool tstamd64.cat。

    -   **/V**选项启用详细的操作，在其中 SignTool 显示成功执行消息和警告消息。

    -   **/S**选项指定的证书存储区的名称 (*PrivateCertStore)* 包含的测试证书。

    -   **/N**选项指定的证书名称 (*Contoso.com(Test))* 安装指定的证书存储区中。

    -   **/T**选项指定 TSA 的 URL (*http://timestamp.verisign.com/scripts/timstamp.dll*) 这将时间戳的数字签名。
        **重要**泄露密钥吊销签名者的代码签名的私钥的情况下包括时间戳提供所需的信息。




-   *tstamd64.cat*指定将对其进行数字签名的编录文件的名称。

tstamd64.cat 指定将对其进行数字签名的编录文件的名称。 根据前面所述，可以打开 cat 文件


7.  *已修改内容摘自*[测试签名的驱动程序通过嵌入式签名](test-signing-a-driver-through-an-embedded-signature.md):

    -   在 64 位版本的 Windows Vista 和更高版本的 Windows 中，内核模式代码签名要求必须具有嵌入式的签名。 这是必需而不考虑是否驱动程序的驱动程序包已进行数字签名的目录文件。

    下面是用于嵌入登录内核模式驱动程序二进制文件的命令。

    ```cpp
    signtool sign  /v  /s  PrivateCertStore  /n  Contoso.com(Test)  /t http://timestamp.verisign.com/scripts/timestamp.dll   amd64\toaster.sys
    ```

    amd64\\toaster.sys 指定将嵌入已签名的内核模式二进制文件的名称。

    在 WDK 的 7.1 安装目录中，toaster 示例将位于 src\\常规\\toaster\\toastpkg\\toastcd\\目录。 Windows 8 或 8.1 WDK 示例是从 Microsoft 下载网站下载。 这些示例不附带 Windows 8 或 8.1 Windows 驱动程序工具包。

    目录文件通过双击 Windows 资源管理器中的文件打开时，您将看到以下屏幕截图。 请注意现在已突出显示"查看签名"。

    ![显示安全目录文件的一般信息的屏幕截图](images/tutorialsecuritycatalogfilegeneraltab.png)

    如果单击"查看签名"，您将看到以下屏幕截图提供从"查看证书"，这将为提供的"安装证书"选项下一步查看选项从对话框本身。 尽管我们提供了以下使用 certmgr.exe 工具将证书安装的首选的命令行选项。

    ![显示有关数字签名的详细信息的常规信息的屏幕截图](images/tutorialdriversignaturedetails.png)

    ![显示有关证书的一般信息的屏幕截图](images/tutorialcertificategeneraltab.png)

对驱动程序现在可以测试签名的计算机或测试计算机上。 如果使用的测试计算机，将驱动程序包复制到计算机保持不变的文件结构。 工具 certmgr.exe 还必须复制到测试计算机。 当使用的测试计算机，将测试签名 Toastpkg 驱动程序包复制到 c:\\toaster 临时文件夹。

以下过程描述在任一计算机上使用测试驱动程序的步骤：

1.  在提升的命令窗口中运行以下命令：

    ```cpp
    bcdedit  /set  testsigning  on
    ```

    重新启动计算机。

2.  *所选部分内容摘自*[到测试计算机上安装测试证书的使用 CertMgr](using-certmgr-to-install-test-certificates-on-a-test-computer.md):

    将证书复制 (*.cer*) 文件，这是用于[测试签名](test-signing-driver-packages.md)驱动程序，到测试计算机。 可以将证书文件复制到测试计算机上的任何目录。

    以下 CertMgr 命令将证书文件中添加证书*CertificateFileName.cer*到受信任的根证书颁发机构的证书存储在测试计算机上：

    ```cpp
    CertMgr.exe /add CertificateFileName.cer /s /r localMachine root
    ```

    以下 CertMgr 命令将证书文件中添加证书*CertificateFileName.cer*到受信任的发行者的证书存储在测试计算机上：

    ```cpp
    CertMgr.exe /add CertificateFileName.cer /s /r localMachine trustedpublisher
    ```

    位置 (*来自* [ **CertMgr**](https://msdn.microsoft.com/library/windows/hardware/ff543411)):

    / 添加 CertificateName

    将证书中指定的证书文件添加到证书存储区。

    /s

    指定的证书存储区是系统存储。

    /r RegistryLocation

    指定系统存储的注册表位置 HKEY_LOCAL_MACHINE 下。

    CertificateStore

    指定证书存储区，trustedpublisher，同样对于"localMachine 根"。

    重新启动计算机。 现在可以运行 Certmgr.msc，并验证 ContosoTest.cer 在上述两个位置中可见。 如果不可见，然后将证书安装另一种方法是打开证书，并在上面的两个节点上安装并重新验证。

3.  验证签名的 cat 文件和 sys 文件。 打开提升的命令窗口，并假定 signtool.exe 可用计算机中，转到驱动程序程序包目录猫、 inf 和 sys 文件所在的位置。 执行以下命令在相应的目录

    从[验证目录文件的 SPC 签名](verifying-the-spc-signature-of-a-catalog-file.md):

    ```cpp
    signtool  verify  /v  /kp  /c  tstamd64.cat  toaster.inf
    ```

    若要检查嵌入登录，请执行以下命令。

    从[验证发布签名驱动程序文件的签名](verifying-the-signature-of-a-release-signed-driver-file.md):

    ```cpp
    signtool  verify  /v  /kp  toaster.sys
    ```

    上面的两个命令将生成一个错误，因为它是测试签名和证书不是受信任的证书。

    ```cpp
    SignTool Error: A certificate chain processed, but terminated in a root certificate which is not trusted by the trust provider.
    ```

    上面的两个验证命令将在版本签名将稍后讨论这非常有用。

    该驱动程序现在已准备好进行安装和测试在测试计算机中。 它始终是建议的以下注册表项已正确设置了在安装过程中收集 setupapi.dev.log 文件 （适用于 Windows Vista 和更高版本操作系统） 中的详细日志。

    ```cpp
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Setup\Loglevel=0x4800FFFF
    ```

    在 %systemroot%\\inf 文件中，setupapi.dev.log 文件重命名之前安装驱动程序。 安装后，新 setupapi.dev.log 创建日志文件将它将包含在安装过程中遇到的重要信息。

    已成功安装驱动程序后，驱动程序的测试可以执行在开发计算机中，或者在测试计算机中。

## <a name="installing-uninstalling-and-loading-the-test-signed-driver-package"></a>安装、 卸载和加载测试签名驱动程序包


在步骤 2 中重新启动系统后，可以安装并加载测试签名驱动程序包。 有四种方法安装的驱动程序包：

1.  通过使用 Dpinst (dpinst.exe) 工具，它是用于安装驱动程序的 WDK 命令行工具，可再发行组件。
2.  通过使用 Devcon (devcon.exe) 工具，它是 WDK 的命令行工具安装驱动程序，但不是可再发行组件。 Devcon 工具的示例代码在 WDK 中提供。 若要重新分发您可以实现你自己的 Devcon 工具的示例代码中，并可以重新分发该工具的版本。
3.  通过使用操作系统提供 Pnputil (pnputil.exe) 工具。
4.  通过使用 Windows 添加硬件向导。

Dpinst 和 Pnputil 之前安装该驱动程序包，而使用 Devcon 和 Windows 添加硬件向导，该驱动程序，以及设备可以安装。 预安装驱动程序可帮助在设备连接到计算机时找到的驱动程序的操作系统。

**若要安装和卸载） 使用 DPInst 驱动程序包**

1.  打开提升的命令窗口，然后将默认目录设置为 c:\\toaster。
2.  Dpinst.exe WDK redist 目录 x86 版本、 的 amd64 版本和 ia64 版本中提供。 将相关版本复制到 c:\\toaster 目录并运行以下命令。

    ```cpp
    dpinst.exe  /PATH  c:\toaster
    ```

    上述命令将安装对应于所有的 inf 文件的所有驱动程序。 此外可以使用"。" 未使用当前目录中引号。 “dpinst.exe /?” 显示有关此工具的所有开关。

    /U 开关上驱动程序 inf 文件将从 DriverStore 资料库中删除驱动程序包 (%systemroot%\\System32\\ DriverStore\\资料库) 提供与关联的设备目录驱动程序已被删除。 使用 Dpinst 工具驱动程序可以只是通过引用该驱动程序的 inf 文件删除。

    ```cpp
    dpinst.exe  /U  toaster.inf
    ```

**若要使用 DevCon 安装驱动程序包**

1.  打开提升的命令窗口，然后将默认目录设置为 c:\\toaster。
2.  Devcon.exe WDK 工具目录 x86 版本、 的 amd64 版本和 ia64 版本中提供。 将相关版本复制到 c:\\toaster 目录并运行以下命令。 此命令将安装该驱动程序，以及设备。

    ```cpp
    devcon.exe  install <inf> <hwid>
    ```

    最好使用引号&lt;hwid&gt;。 对于 toaster 示例中，它将是：

    ```cpp
    devcon.exe  install  c:\toaster\toaster.inf  “{b85b7c50-6a01-11d2-b841-00c04fad5171}\MsToaster”
    ```

    可以使用 Devcon 工具使用"删除"开关移除某个设备。 “devcon.exe /?” 显示有关此工具的所有开关。 若要获取特定信息，请使用交换机上"帮助"应如下所示的"删除"交换机添加。

    ```cpp
    devcon.exe help remove
    ```

    上述命令提供以下信息。

    删除具有指定 ID 的硬件或实例的设备 仅在本地计算机上有效。 （若要重新启动在必要时，包含-r。）

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

    移除某个设备后，若要删除该驱动程序，两个命令是必需的。 使用"dp_enum"开关使用第一个命令查找驱动程序 inf 文件名称对应于在计算机中安装的驱动程序包。

    ```cpp
    devcon  dp_enum
    ```

    此命令将显示所有文件的列表 oemNnn.inf 对应驱动程序包，其中 Nnn 是带类信息和提供信息的十进制数字，如下所示。

    ```cpp
    oem39.inf
        Provider: Intel
        Class: Network adapters
    oem4.inf
        Provider: Dell
        Class: ControlVault Device
    ```

    若要从 DriverStore 删除相应的驱动程序包，请使用如下所示对 Intel"网络适配器"下一步命令驱动程序：

    ```cpp
    devcon.exe dp_delete oem39.inf
    ```

**若要使用 PnpUtil 安装驱动程序包**

1.  打开提升的命令窗口，然后将默认目录设置为 c:\\toaster。
2.  运行以下命令，它将显示所有可用的参数。 使用的开关是很容易理解，无需显示任何示例。
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

**若要使用添加硬件向导安装驱动程序包**

1.  打开提升的命令窗口
2.  运行 hdwwiz.cpl 以启动添加硬件向导，请转到第二页旁边单击
3.  选择高级选项，然后单击下一步
4.  选择显示在列表框中的所有设备，单击下一步
5.  选择从磁盘安装选项
6.  输入包含在 c： 驱动器的文件夹的路径\\toaster 驱动程序包
7.  选择的 inf 文件，然后单击打开
8.  单击“确定”
9.  在接下来的两页中，单击下一步，然后单击完成以完成安装

**验证测试签名驱动程序正常运行**

若要验证 Toastpkg 正常运行：

1.  启动设备管理器
2.  从设备列表中选择 Toaster。 有关示例，请参阅以下屏幕截图。

    ![设备管理器中显示 toaster 设备的屏幕截图](images/tutorialtoasterpackageindevicemgr.png)

3.  若要打开驱动程序的属性对话框，请双击 Toaster 程序包示例 Toaster
4.  若要确认 Toaster 正常运行，以在常规选项卡上，检查状态中

设备管理器可以用于从属性对话框中卸载设备和驱动程序。

**如何进行故障排除测试签名的驱动程序**

请参阅[解决驱动程序签名安装](troubleshooting-driver-signing-installation.md)如果遇到任何困难这些过程。









