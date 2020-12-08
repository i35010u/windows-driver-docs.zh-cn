---
title: 排查驱动程序签名安装问题
description: 安装版本签名驱动程序与在测试签名中安装、卸载和加载 Test-Signed 驱动程序包中所述相同，只是安装时需要执行两个额外步骤，使用此处所述的任何一种方法来安装。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a3bb4825ed6d49fdce2a37a4530a3844dd1bf41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828599"
---
# <a name="troubleshooting-driver-signing-installation"></a>排查驱动程序签名安装问题


安装版本签名驱动程序与在 [测试签名](test-signing.md)中 **安装、卸载和加载 Test-Signed 驱动程序包** 中所述相同，只是安装时需要执行两个额外步骤，使用此处所述的任何一种方法来安装。 使用 "添加硬件向导" 安装版本签名的驱动程序会显示其他两个步骤，其中包括一些常见安装问题。

1.  打开提升的命令窗口
2.  运行 hdwwiz.cpl 以启动添加硬件向导，然后选择 "下一步" 以前往第二页
3.  选择 "高级" 选项并选择 "下一步"
4.  从列表框中选择 "显示所有设备"，然后选择 "下一步"
5.  选择 "具有磁盘" 选项
6.  输入包含 C： \\ toaster 驱动程序包的文件夹的路径
7.  选择 inf 文件，然后选择 "打开"。
8.  选择“确定”
9.  在接下来的两页中选择 "下一步"，然后选择 "完成" 以完成安装
10. 在询问 "是否要安装此设备软件？" 的对话框中选择 "安装"
11. 选择 "完成" 以完成安装。

步骤10显示了下面的 "Windows 安全性" 对话框。

![显示 "windows 安全" 对话框的屏幕截图](images/tutorialwindowssecurityinstalldialog.png)

如果再次安装了驱动程序，或者如果出于任何原因删除了驱动程序，则选中该复选框将不再在计算机上显示此对话框。

**注意**  系统会根据用于对目录进行签名的 SPC 验证发行者信息是否准确。 如果发布服务器信任级别是未知的，则对于 Contoso .com，系统将显示该对话框。 要继续安装，用户必须选择 "安装"。 有关信任和驱动程序安装的详细信息，请参阅 [代码签名最佳做法](/previous-versions/windows/hardware/design/dn653556(v=vs.85))。

 

未签名的驱动程序将显示以下对话框，该对话框允许用户安装未签名的驱动程序， (这在 x64 版本的 Windows) 中可能不起作用。

![显示 "windows 安全警告" 对话框的屏幕截图](images/tutorialwindowssecurityinstallwarning.png)

## <a name="verify-that-the-release-signed-driver-is-operating-correctly"></a>验证 Release-Signed 驱动程序是否正常运行


使用设备管理器查看 (测试签名驱动程序) 前面介绍的驱动程序属性。 下面是屏幕截图，显示驱动程序是否正常运行。

![在设备管理器中显示 toaster 设备的屏幕截图](images/tutorialtoasterpackageindevicemgr.png)

## <a name="troubleshoot-release-signed-drivers"></a>Release-Signed 驱动程序故障排除


下面列出了用于排查加载已签名或测试签名驱动程序的问题的几种常见方法：

-   使用 "添加硬件向导" 或设备管理器来检查是否已加载并签署了驱动程序，如 **验证 Test-Signed 驱动程序是否正常运行**[测试签名](test-signing.md)中所述。
-   打开 \\ 驱动程序安装后在 Windows inf 目录中创建的 setupapi.log 文件。 请参阅设置注册表项和重命名 setupapi.log 文件部分，然后再安装驱动程序。
-   检查 Windows 安全审核日志和代码完整性事件日志。

## <a name="analyzing-the-setupapidevlog-file"></a>分析 Setupapi.log 文件


如之前所述，将记录任何驱动程序安装信息 (追加) 到 Windows inf 目录中的 setupapi.log 文件。 \\ 如果在安装驱动程序之前重命名该文件，则将生成新的日志文件。 使用新的驱动程序安装时，新的日志文件更容易搜索重要的日志。 该日志文件将在记事本应用程序中打开。

第一个最左侧的列可能有一个感叹号 "！" 或多个感叹号 "!!!"。 单标记是一条警告消息，但三个感叹号表示失败。

安装使用 CA 供应商提供的 SPC 证书签名的驱动程序包版本时，你将看到以下单个感叹号。 这些是有关 cat 文件尚未验证的警告。

```cpp
!    sig:                Verifying file against specific (valid) catalog failed! (0x800b0109)
!    sig:                Error 0x800b0109: A certificate chain processed, but terminated in a root certificate which is not trusted by the trust provider.
     sig:                Success: File is signed in Authenticode(tm) catalog.
     sig:                Error 0xe0000242: The publisher of an Authenticode(tm) signed catalog has not yet been established as trusted.
```

请参阅驱动程序安装的步骤10，然后选择 "安装" 按钮。 你将看到下面的日志，在大多数情况下，这意味着驱动程序将安装并加载正常。 设备管理器不会报告驱动程序的任何错误或黄色惊叹号。

```cpp
!    sto:           Driver package signer is unknown but user trusts the signer.
```

如果日志文件中还显示以下错误日志，则可能不会加载驱动程序。

Setupapi.log 文件也报告以下错误：

```cpp
!!!  dvi:                          Device not started: Device has problem: 0x34: CM_PROB_UNSIGNED_DRIVER.
```

请注意，0x34 赋是代码52。

若要进行故障排除，请查看日志文件并查找驱动程序二进制文件旁边的感叹号。 `signtool verify`对 cat 文件和其他嵌入的已签名二进制文件运行该命令。

通常，日志文件信息足以解决问题。 如果上述检查未能找到根本原因，请检查 Windows 安全审核日志和代码完整性事件日志，如下一节中所述。

如果服务二进制文件复制尚未提交，但操作系统尝试启动该服务，则驱动程序服务将无法启动。 如果发生这种情况，请使用 setupapi.log 文件检查驱动程序文件复制和提交时间信息。 重启应成功启动服务。 请参阅下面的日志文件中的示例操作序列。

```cpp
>>>  Section start 2014/02/08 14:54:56.463
```

稍后在下一次：

```cpp
!    inf:                     Could not start service 'toaster'.
```

接下来，我们有文件复制操作：

```cpp
<snip>
flq:                {FILE_QUEUE_COPY}
     flq:                     CopyStyle      - 0x00000000
     flq:                     SourceRootPath - 'C:\Windows\System32\DriverStore\FileRepository\Toaster.inf_amd64_d9b35403a0fe4391\'
     flq:                     SourceFilename - 'toaster.exe'
     flq:                     TargetDirectory- 'C:\Windows\System32\drivers'
     flq:                     TargetFilename - 'toaster.exe'
```

接下来将提交文件。 将结束时间与开始时间进行比较。

```cpp
flq:           {_commit_file_queue} 14:54:56.711
<snip>
     flq:                     {_commit_copyfile}
     flq:                          Copying 'C:\Windows\System32\DriverStore\FileRepository\Toaster.inf_amd64_d9b35403a0fe4391\o2flash.exe' to 'C:\Windows\System32\drivers\o2flash.exe'.
     flq:                          CopyFile: 'C:\Windows\System32\DriverStore\FileRepository\Toaster.inf_amd64_d9b35403a0fe4391\o2flash.exe' to 'C:\Windows\System32\drivers\SETDA81.tmp'
     flq:                          MoveFile: 'C:\Windows\System32\drivers\SETDA81.tmp' to 'C:\Windows\System32\drivers\toaster.exe'
     cpy:                          Applied 'OEM Legacy' protection on file 'C:\Windows\System32\drivers\toaster.exe'.
     flq:                          Caller applied security to file 'C:\Windows\System32\drivers\toaster.exe'.
     flq:                     {_commit_copyfile exit OK}
<snip>
     sto:      {Configure Driver Package: exit(0x00000bc3)}
     ndv:      Restart required for any devices using this driver.
<snip>
<<<  Section end 2014/02/08 14:54:57.024
<<<  [Exit status: SUCCESS]
```

上面的示例是在 Windows 7 中工作良好但在 Windows 8.0 和8.1 中出现故障的驱动程序更新，导致发现 bug。

## <a name="using-the-windows-security-audit-log"></a>使用 Windows 安全审核日志


如果由于缺少有效的签名而导致驱动程序无法加载，则会将其记录为审核失败事件。 审核失败事件记录在 Windows 安全日志中，指示代码完整性无法验证驱动程序文件的映像哈希。 日志项包含驱动程序文件的完整路径名称。 仅当本地安全审核策略启用了系统失败事件的日志记录时，才会生成安全日志审核事件。

**注意**  必须显式启用安全审核日志。 有关详细信息，请参阅 [附录3：启用代码完整性事件日志记录和系统审核](appendix-3--enable-code-integrity-event-logging-and-system-auditing.md)。

 

检查安全日志：

1.  打开提升的命令窗口。
2.  若要启动 Windows 事件查看器，请运行 Eventvwr.exe。 也可以从 "控制面板" 的 "计算机管理" 应用程序中启动事件查看器。
3.  打开 Windows 安全审核日志。
4.  请检查日志中是否存在事件 ID 为5038的系统完整性事件。
5.  选择并按住 (或右键单击日志条目) ，然后选择 "事件属性" 以显示其 "事件属性" 对话框，该对话框提供事件的详细说明。

下面的屏幕截图显示了由未签名的 Toaster.sys 文件引起的安全审核日志事件的 "事件属性" 对话框。

!["事件属性" 对话框的屏幕截图 showig](images/tutorialeventprops.png)

## <a name="using-the-code-integrity-event-operational-event-log"></a>使用代码完整性事件操作事件日志


如果由于未对驱动程序进行签名或生成了图像验证错误而无法加载该驱动程序，则代码完整性将在代码完整性操作事件日志中记录这些事件。 代码完整性操作事件始终处于启用状态。

可以通过事件查看器查看代码完整性事件。

## <a name="to-examine-the-code-integrity-operational-log"></a>检查代码完整性操作日志


1.  打开提升的命令窗口。
2.  若要启动 Windows 事件查看器，请运行 Eventvwr.exe。 也可以从 "计算机管理" 控制面板应用程序中启动事件查看器。
3.  打开 Windows 代码完整性日志。
4.  选择并按住 (或右键单击) 日志条目，然后选择 "事件属性" 以显示其 "事件属性" 对话框，该对话框提供事件的详细说明。

下面的屏幕截图显示了由未签名的 Toaster.sys 文件引起的代码完整性操作日志事件的 "事件属性" 对话框。

![显示事件查看器的屏幕截图](images/tutorialeventvwr.png)

## <a name="using-the-informational-events-in-the-code-integrity-verbose-log"></a>使用代码完整性详细日志中的信息性事件


代码完整性信息日志的详细视图跟踪所有内核模式映像验证检查的事件。 这些事件显示系统上加载的所有驱动程序的成功图像验证。

启用代码完整性详细视图：

1.  开始事件查看器，如前面的示例中所示。
2.  选择 "代码完整性" 节点，使其成为焦点。
3.  选择并按住 (或右键单击) 代码完整性 "，然后从快捷菜单中选择" 查看项 "。
4.  选择 "显示分析和调试日志"。 这将创建一个具有两个附加节点的子树： "操作" 和 "详细"。
5.  选择并按住 (或右键单击) 详细 "节点，然后从快捷菜单中选择" 属性 "。
6.  在 "常规" 选项卡上，选择 "启用日志记录" 以启用详细日志记录模式。
7.  重新启动系统以重新加载所有内核模式的二进制文件。
8.  重新启动后，打开 MMC "计算机管理" 管理单元，并查看代码完整性详细事件日志。

[附录4：驱动程序签名问题](appendix-4--driver-signing-issues.md)中介绍了几个额外的已知驱动程序签名问题。

 

