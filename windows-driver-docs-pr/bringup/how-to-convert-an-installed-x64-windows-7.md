---
title: 如何转换已安装的 x64 Windows 7 系统
description: 如何转换已安装的 x64 Windows 7 系统
ms.date: 01/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8c57b53240097f75079b35a1a25e9f18cdf384e9
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186047"
---
# <a name="how-to-convert-an-installed-x64-windows-7-system"></a>如何转换已安装的 x64 Windows 7 系统

以下步骤旨在供 ITPro 在需要从旧的 MBR + CSM 转换到 UEFI + GPT 的情况下使用。 通常，此过程从安装了 Windows 7 x64 的系统开始。

对于 x86 OS 系统，请参阅 [固件 WEG 常见问题解答](frequently-asked-questions.md) 中的 "有关32位和64位 UEFI 的依赖关系是什么？" 部分。

已在 BIOS 模式中安装到启用了 CSM 的传统 MBR 启动盘，并知道或已检查 OEM 以确保系统具有以下各项：

1. 能够启用和禁用 CSM
1. 具有 UEFI 固件 2.3.1 c 或更高版本
1.  (安全启动、要求 HVCI 和 Credential Guard) 的安全功能都已在系统上配置了所有正确的组件。
    > [!NOTE]
    > Microsoft 目前没有一种机制，无需先擦除或清理现有文件系统并在清理磁盘上创建新文件系统，即可将旧的 MBR 启动磁盘转换为 GPT 磁盘。

例如，你将需要使用 Diskpart.exe 来 **清理** 现有分区，然后在该磁盘上运行 **转换 GPT** 命令。 **Clean**命令将擦除整个磁盘。

1. 确保所有数据都已从主启动设备备份，并且用户或 ITPro 已确认主启动设备为磁盘0
1. 已完全备份主启动设备 (会擦除磁盘上保留的任何数据) 
1. 重新启动到 BIOS (与制造商联系，以获取将 BIOS 启动模式切换到 UEFI 启动模式的步骤) aand 切换到 UEFI + CSM
1. 启动到包含 x64 WinPE 的 USB 闪存驱动器
1. 在启动到 WinPE 后，请在命令提示符下执行以下操作：
    1. 打开 Diskpart.exe
    1. 选择磁盘0
    1. 列表 par
    1. 列出 "卷 <=" 以确定当前的驱动器号，以便知道现有 OS 的分配位置 (确定 OS 的驱动器号，稍后用到) 
    1. 转换 GPT
    1. 选择分区1
    1. create par EFI size = 800 (mg) 
    1. format fs = fat32 标签 = 系统
    1. 分配字母 S
    1. 创建 par MSR
    1. 列表 par
    1. exit
1. 返回命令提示符下，键入以下命令：
    1. ：
    1. BCDboot c： \\ windows/s s：/F UEFI
       > [!NOTE]
       > 这是上面的步骤 c 和 d 中标识的驱动器号
    1. dir/a
    1. 应看到： \\ EFI
    1. 重新启动并尝试启动到 OS

## <a name="verify-system-is-booted-in-uefi-mode"></a>验证是否在 UEFI 模式下启动系统

使用以下方法之一验证系统是否在 UEFI 模式下启动。

### <a name="msinfo32"></a>MSINFO32

在 Windows 10 系统上：

1. 按 \<Windows key\>  +  \<R\> 打开 "**运行**" 对话框
1. 键入 Msinfo32 并单击 **"确定"**

默认情况下，系统摘要页面将打开。

查找以下信息：

![系统摘要页面](images/system-summary-page.png)

若要以管理员身份运行，请使用以下步骤：

1. 按 \<Windows key\>  +  \<R\> 打开 "**运行**" 对话框
1. 开始键入 "系统信息"

如果突出显示**系统信息**、保持 \<CTRL\>  +  \<SHIFT\> 和点击 \<ENTER\> ，或使用鼠标右键单击并选择 "**以管理员身份运行**"。

用户访问控制 (UAC) 会提示你，其中包含以下消息： **是否希望此应用对你的桌面进行更改？**

### <a name="bcdedit"></a>BCDEDIT

在 Windows 7 及更高版本系统上：

1. 启动提升的命令提示符
1. 运行 "BCDedit/enum {current}"
    > [!NOTE]
    > 如果从 WinPE 启动，请在 BCDedit.exe 中使用 "/store" 开关。
    > 如果有 UEFI，路径将显示 Winload.exe。
    > 如果您有 CSM，路径将显示示例输出中列出 Winload.exe。

#### <a name="sample-output"></a>示例输出

```cmd
Windows Boot Loader
-------------------
identifier {current}
device partition=C:
path \WINDOWS\system32\winload.efi
```

### <a name="notepad-and-setupactlog"></a>记事本和 SETUPACT.LOG。日志

1. 启动提升的命令提示符
1. 运行 "notepad c： \\ windows \\ panther \\ setupact.log"
1. 按 \<CTRL\>  +  \<F\> 查找 (或搜索) 
1. 搜索 "Callback \_ BootEnvironmentDetect"

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

你可能需要咨询 OEM 以了解特定系统上的配置详细信息。

> [!WARNING]
> 使用 diskpart.exe 或安装程序清理或擦除硬盘驱动器分区信息将全部损坏磁盘上的数据。 在进行任何更改之前，请咨询计算机制造商有关出厂映像恢复方法或数据备份选项的情况。

## <a name="related-resources"></a>相关资源

[建议的基于 UEFI 的磁盘分区配置](/previous-versions/windows/it-pro/windows-7/dd744301(v=ws.10))

[Win7 备份程序、系统设置和文件](https://support.microsoft.com/help/17127/windows-back-up-restore#1TC=windows-7)

[Win7 通过 Windows 7 备份保护你的文件和 PC](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/bg-p/FileCAB)