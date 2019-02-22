---
title: 如何将转换已安装的 x64 Windows 7 系统
description: 如何将转换已安装的 x64 Windows 7 系统
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: cffd5cfbf35961844f840f4b4b6e40c8e8e1107e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541766"
---
# <a name="how-to-convert-an-installed-x64-windows-7-system"></a>如何将转换已安装的 x64 Windows 7 系统

以下步骤适用于使用由 it 专业人员在方案中需要从旧版 MBR + CSM 转换为 UEFI + GPT 的哪个位置。 通常，此过程开始 Windows 7 安装 x64 的系统。

适用于 x86 OS 系统，请参阅中的部分[固件 WEG 常见问题解答](frequently-asked-questions.md)有关"什么是对 32 位与的依赖关系。64 位 UEFI？"。

在 BIOS 模式下才能旧版 MBR 启动盘随 CSM 启用，和你了解或已与 OEM 以确保系统具有以下检查：

1. 可启用和禁用 CSM
1. 具有 UEFI 固件 2.3.1c 或更高版本
1. 你感兴趣 （安全启动、 Device Guard 和 Credential Guard） 的安全功能具有已在系统上配置的所有正确组件。
    > [!NOTE]
    > Microsoft 当前不具有一种机制来将旧版 MBR 启动磁盘转换为 GPT 磁盘，而无需第一个擦除或清除现有的文件系统和清理磁盘上创建新的文件系统。

例如，你将需要使用到 Diskpart.exe**干净**运行之前的现有分区**convert GPT**命令该磁盘上。 **干净**命令将擦除整个磁盘。

1. 确保所有数据都备份从主引导设备和用户或 it 专业人员已经确认该为主引导设备是磁盘 0
1. 为主引导设备已完全备份最多 （将擦除磁盘上剩余的任何数据）
1. 重新启动到 BIOS （联系制造商为到 UEFI 引导模式切换 BIOS 启动模式的步骤） aand 切换到 UEFI + CSM
1. 为包含 x64 的 USB 闪存驱动器启动 WinPE
1. 之后在命令提示符下启动到 WinPE，：
    1. 打开 Diskpart.exe
    1. 选择磁盘 0
    1. 列表 par
    1. list VOL < = 来标识当前的驱动器号，因此如果您知道现有 OS 已分配的 （标识为用更高版本的操作系统的驱动器号）
    1. 转换 GPT
    1. 选择分区 1
    1. 创建 par EFI size = 800 (mg)
    1. format = fat32 标签 = 系统
    1. 分配字母 S
    1. 创建 par MSR
    1. 列表 par
    1. exit
1. 返回在命令提示符处，键入所示：
    1. s:
    1. BCDboot c:\\windows /s s: /f UEFI
       > [!NOTE]
       > 这是驱动器号标识在步骤 c 和 d 更高版本
    1. dir/a
    1. 应会看到 s:\\EFI
    1. 重新启动并尝试启动到 OS

## <a name="verify-system-is-booted-in-uefi-mode"></a>验证在 UEFI 模式下启动系统

若要验证系统的以下方法之一在 UEFI 模式下启动时使用。

### <a name="msinfo32"></a>MSINFO32

在 Windows 10 系统：

1. 按\<Windows 键\> + \<R\>以打开**运行**对话框
1. 键入 Msinfo32，然后单击**确定**

默认情况下，将打开系统摘要页。

查找以下信息：

![系统摘要页](images/system-summary-page.png)

若要以管理员身份运行，请使用以下步骤：

1. 按\<Windows 键\> + \<R\>以打开**运行**对话框
1. 开始键入"系统信息"

如果**系统信息**是突出显示，存放\<CTRL\> + \<SHIFT\>并点击\<ENTER\>，或使用鼠标执行右键单击然后选择**以管理员身份运行**。

系统会提示用户访问控制 (UAC) 并显示以下消息：**此应用对您的桌面进行更改吗？**

### <a name="bcdedit"></a>BCDEDIT

在 Windows 7 和更高版本的系统：

1. 启动提升的命令提示符
1. 运行"BCDedit /enum {当前}"
    > [!NOTE]
    > 如果从 WinPE 启动，则在 BCDedit.exe 中使用"/ 存储"开关。
    > 如果你有 UEFI，路径将显示 Winload.efi。
    > 如果您有 CSM，路径将如下所示的示例输出显示 Winload.exe。

#### <a name="sample-output"></a>示例输出

```cmd
Windows Boot Loader
-------------------
identifier {current}
device partition=C:
path \WINDOWS\system32\winload.efi
```

### <a name="notepad-and-setupactlog"></a>记事本和 SETUPACT。日志

1. 启动提升的命令提示符
1. 运行"记事本 c:\\windows\\panther\\setupact.log"
1. 按\<CTRL\> + \<F\>查找 （或搜索）
1. 搜索"回调\_BootEnvironmentDetect"

    - 结果将如下所示：

        ```cmd
        Callback_BootEnvironmentDetect:FirmwareType 1

        Callback_BootEnvironmentDetect: Detected boot environment: BIOS
        ```

        或

        ```cmd
        Callback_BootEnvironmentDetect:FirmwareType 2

        Callback_BootEnvironmentDetect: Detected boot environment: UEFI
        ```

您可能需要的 OEM 特定系统上的配置详细信息，请咨询。

> [!WARNING]
> 使用 diskpart.exe 或安装程序来进行清理或擦除硬盘驱动器分区信息将所有销毁的数据磁盘上。 请咨询有关工厂映像恢复方法或数据备份选项进行任何这些更改之前 PC 制造商。

## <a name="related-resources"></a>相关资源

[建议使用基于 UEFI 的磁盘分区配置](https://technet.microsoft.com/library/dd744301)

[Win7 备份程序、 系统设置和文件](http://windows.microsoft.com/windows/back-up-programs-system-settings-files#1TC=windows-7)

[Win7 保护文件和使用 Windows 7 备份 PC](https://blogs.technet.microsoft.com/filecab/2009/10/23/protect-your-files-and-pc-with-windows-7-backup/)
