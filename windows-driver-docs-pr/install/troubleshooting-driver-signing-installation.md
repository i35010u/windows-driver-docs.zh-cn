---
title: 排查驱动程序签名安装问题
description: 安装已发布签名的驱动程序是在安装、 卸载和加载 Test-Signed 驱动程序包中测试签名，除了需要安装有使用任何所述的四个方法时的其他两个步骤中所述相同。
ms.assetid: 36624611-1FE6-4B88-B785-44D6A81F61FF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c65fdb85ef48cec5515b9f3029eeb42b1797e588
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339582"
---
# <a name="troubleshooting-driver-signing-installation"></a>排查驱动程序签名安装问题


安装已发布签名的驱动程序是在中所述的相同**安装、 卸载和加载 Test-Signed 驱动程序包**中[测试签名](test-signing.md)，除了其他两个步骤所需时安装那里使用任何所述的四个方法。 使用添加硬件向导安装已发布签名的驱动程序显示了其他两个步骤，包括的一些常见安装问题。

1.  打开提升的命令窗口
2.  运行 hdwwiz.cpl 以启动添加硬件向导，请转到第二页旁边单击
3.  选择高级选项，然后单击下一步
4.  选择显示在列表框中的所有设备，单击下一步
5.  选择从磁盘安装选项
6.  输入包含在 c： 驱动器的文件夹的路径\\toaster 驱动程序包
7.  选择的 inf 文件，然后单击打开
8.  单击“确定”
9.  在接下来的两页中，单击下一步，然后单击完成以完成安装
10. 单击安装对话框，询问"您想要安装此设备软件？"
11. 单击完成以完成安装。

步骤 10 显示了以下 Windows 安全对话框。

![显示 windows 安全性对话框的屏幕截图](images/tutorialwindowssecurityinstalldialog.png)

选中复选框将显示此对话框中的计算机中如果再次安装该驱动程序是否出于任何原因删除驱动程序。

**请注意**  系统将验证发布服务器信息是准确基于用于对目录进行签名的 SPC。 如果发布服务器的信任级别未知-Contoso.com—the 系统显示对话框中一样将为 true。 若要继续安装，用户必须单击安装。 有关信任和驱动程序安装的详细信息，请参阅[代码签名最佳做法](https://msdn.microsoft.com/library/windows/hardware/dn653556)。

 

未签名的驱动程序而将显示以下对话框中，这样用户就可以安装未签名的驱动程序，这可能无法在 x64 版本的 Windows。

![显示 windows 安全警告对话框的屏幕截图](images/tutorialwindowssecurityinstallwarning.png)

## <a name="verify-that-the-release-signed-driver-is-operating-correctly"></a>验证正确运行 Release-Signed 驱动程序


使用设备管理器查看驱动程序属性，如之前所述测试签名驱动程序方面。 下面是屏幕截图显示如果驱动程序可正常工作。

![设备管理器中显示 toaster 设备的屏幕截图](images/tutorialtoasterpackageindevicemgr.png)

## <a name="troubleshoot-release-signed-drivers"></a>对版本签名的驱动程序进行故障排除


以下列表提供了几个常见的方式来加载已签名的问题进行故障排除或测试签名的驱动程序：

-   使用添加硬件向导或设备管理器检查驱动程序是否已加载和签名，如中所述**验证 Test-Signed 驱动程序是操作系统正确**的[测试签名](test-signing.md)。
-   打开 Windows 中创建的 setupapi.dev.log 文件\\inf 目录后驱动程序安装。 请参阅上设置注册表项和安装驱动程序之前 setupapi.dev.log 文件重命名部分。
-   检查 Windows 安全审核日志和代码完整性事件日志。

## <a name="analyzing-the-setupapidevlog-file"></a>分析 Setupapi.dev.log 文件


如之前所述，将 Windows 中的 setupapi.dev.log 文件 （追加） 记录的任何驱动程序安装信息\\inf 目录。 如果之前安装驱动程序，重命名该文件，将生成一个新的日志文件。 新的日志文件将更轻松地查找重要的新的驱动程序安装日志。 在记事本应用程序中打开该日志文件。

第一个保留大多数列可能有一个感叹号"！" 或多个感叹号"!!!"。 单个标记类型的一条警告消息，但三重感叹号将是发生故障的征兆。

你将看到以下单个标记了感叹号安装使用 CA 供应商签名的驱动程序包版本时提供的 SPC 证书。 它们只是警告，以指示，cat 文件尚未验证尚未。

```cpp
!    sig:                Verifying file against specific (valid) catalog failed! (0x800b0109)
!    sig:                Error 0x800b0109: A certificate chain processed, but terminated in a root certificate which is not trusted by the trust provider.
     sig:                Success: File is signed in Authenticode(tm) catalog.
     sig:                Error 0xe0000242: The publisher of an Authenticode(tm) signed catalog has not yet been established as trusted.
```

如果您现在到步骤 10 驱动程序安装的参考，并单击"安装"按钮，你将看到以下日志后，在大多数情况下，驱动程序将安装并正常加载。 设备管理器将不报告任何错误或驱动程序，显示黄色感叹号。

```cpp
!    sto:           Driver package signer is unknown but user trusts the signer.
```

尽管上述为止获取驱动程序可能不会加载如果另请参阅以下的错误记录在日志文件中。

Setupapi.dev.log 文件也报告了以下错误：

```cpp
!!!  dvi:                          Device not started: Device has problem: 0x34: CM_PROB_UNSIGNED_DRIVER.
```

请注意，0x34 代码 52。

此时可能会返回在日志文件，并尝试查找是否用任何感叹号发出信号任何驱动程序二进制文件。 可以提供一些线索。 否则，甚至应运行所述的"signtool 验证"命令之前 cat 文件和其他嵌入签名的二进制文件以确保签名驱动程序中不存在任何问题。

大多数情况下日志文件信息就足以解决此问题。 如果上述检查未能找到根本原因，然后下一种方法是检查 Windows 安全审核日志和代码完整性事件日志即下一节中所述。

Setupapi.dev.log 文件还可帮助跟踪驱动程序文件复制和提交时间信息，以防如果找到一个驱动程序服务无法启动与服务二进制文件复制尚未提交但操作系统尝试启动服务。 但重新启动已成功启动服务。 请参阅下面的日志文件中的操作序列。

```cpp
>>>  Section start 2014/02/08 14:54:56.463
```

下一步，在更高版本时：

```cpp
!    inf:                     Could not start service 'toaster'.
```

然后，我们可以文件复制操作：

```cpp
<snip>
flq:                {FILE_QUEUE_COPY}
     flq:                     CopyStyle      - 0x00000000
     flq:                     SourceRootPath - 'C:\Windows\System32\DriverStore\FileRepository\Toaster.inf_amd64_d9b35403a0fe4391\'
     flq:                     SourceFilename - 'toaster.exe'
     flq:                     TargetDirectory- 'C:\Windows\System32\drivers'
     flq:                     TargetFilename - 'toaster.exe'
```

接下来，该文件是已提交。 比较开始时间的结束时间。

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

以上是 bug 的驱动程序更新的 Windows 7 中正常工作，但是在 Windows 8.0 和 8.1，发现导致失败的情况。

## <a name="using-the-windows-security-audit-log"></a>使用 Windows 安全审核日志


如果驱动程序未能加载，因为它不具备有效的签名，则审核失败事件会记录在 Windows 安全日志，该值指示代码完整性无法验证驱动程序文件的映像哈希。 日志条目包括驱动程序文件的完整路径名称。 仅当本地安全审核策略，则系统失败事件的记录生成安全日志审核事件。

**请注意**  必须显式启用安全审核日志。 有关详细信息，请参阅[附录 3:启用代码完整性事件日志记录和审核系统](appendix-3--enable-code-integrity-event-logging-and-system-auditing.md)。

 

安全日志中检查：

1.  打开提升的命令窗口。
2.  若要启动 Windows 事件查看器，请运行 Eventvwr.exe。 也可以从控件面板计算机管理应用程序启动事件查看器。
3.  打开 Windows 安全审核日志。
4.  检查具有事件 ID 为 5038 的系统完整性事件日志。
5.  双击日志项以显示其事件属性对话框中，提供事件的详细的说明。

下面的屏幕快照显示了已导致的未签名的 Toaster.sys 文件的安全审核日志事件事件属性对话框。

![屏幕截图 showig 事件属性对话框](images/tutorialeventprops.png)

## <a name="using-the-code-integrity-event-operational-event-log"></a>使用代码完整性事件操作事件日志


如果驱动程序未能加载，因为它未签名或生成映像验证错误，代码完整性代码完整性 operational 事件日志中记录事件。 始终启用代码完整性操作事件。

可以使用事件查看器查看的代码完整性事件。

## <a name="to-examine-the-code-integrity-operational-log"></a>代码完整性操作日志中检查


1.  打开提升的命令窗口。
2.  若要启动 Windows 事件查看器，请运行 Eventvwr.exe。 也可以从计算机管理控制面板应用程序启动事件查看器。
3.  打开 Windows 代码完整性日志。
4.  双击日志项以显示其事件属性对话框中，提供事件的详细的说明。

下面的屏幕快照显示了已导致的未签名的 Toaster.sys 文件的代码完整性运行日志事件事件属性对话框。

![显示在事件查看器的屏幕截图](images/tutorialeventvwr.png)

## <a name="using-the-informational-events-in-the-code-integrity-verbose-log"></a>使用中的代码完整性详细日志的信息性事件


代码完整性信息性日志的详细视图跟踪针对所有内核模式映像验证检查的事件。 这些事件显示在系统上的所有驱动程序加载的图像成功验证。

若要启用代码完整性详细视图：

1.  启动事件查看器中，如前面的示例中所示。
2.  单击代码完整性节点以使其获得焦点。
3.  右键单击代码完整性，并从快捷菜单中选择的视图项。
4.  选择显示分析和调试日志。 这将创建具有两个其他节点的子树：操作和 Verbose。
5.  右键单击详细节点，然后从快捷菜单中选择的属性。
6.  在常规选项卡，选择启用日志记录，若要启用详细日志记录模式。
7.  重新启动系统重新加载所有内核模式二进制文件。
8.  在重启之后, 打开计算机管理 MMC 管理单元并查看代码完整性详细事件日志。

中介绍了几个其他已知的驱动程序签名问题[附录 4:驱动程序签名问题](appendix-4--driver-signing-issues.md)。

 

 





