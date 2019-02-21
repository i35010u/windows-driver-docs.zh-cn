---
title: 旧方法-Windows 10 版本 1607年及更早版本
description: 旧方法-Windows 10 版本 1607年及更早版本
ms.date: 05/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 739b8a90c89372f5e3175591cfa971b4e3116df0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555825"
---
# <a name="old-method---windows-10-version-1607-and-earlier"></a>旧方法-Windows 10 版本 1607年及更早版本

在升级方案 (Windows 7 到 Windows 10) 中，技术人员需要能够更改 OS 和固件从 Windows 7 SPn 旧版启动 + CSM 到 Win10 UEFI-CSM （减去 CSM)，包含 Windows 7 SPn x64 安装媒体。

此过程可能如下所示 （详见下文）：

1. 请咨询 OEM 上可用于此固件或主板的安全选项。 并非所有的安全选项可在某些固件或母板上。

2. 备份整个主要启动磁盘 （即在保存计划） 中的所有数据。

    > [!NOTE]
    > 建议创建映像或无 OEM 恢复介质。

3. 创建可启动 x64 WinPE 的 USB 闪存驱动器 (UFD) 或 CD/DVD。

4. 重新启动到固件用户界面 (UI) 和切换设置为到 UEFI 启动 （如果需要启动返回到 Win7 时，将需要 CSM 现在已启用）。

5. DVD/CD/USB 设备上的启动到 WinPE (**安全引导**必须禁用启动到备用的启动设备)。

6. 使用 Diskpart.exe 擦除干净主启动磁盘。

    > [!NOTE]
    > 如果存在多个磁盘，则确认该磁盘 0 已为主引导设备之前清除该磁盘，因为在磁盘上，此过程将擦除所有数据。

7. 此时，有几个选项，IT 人员可能需要与系统 OEM 联系以获取特定的说明配置选项。

    a.  插入全新安装介质，然后运行 setup.exe。 则可能在安装过程将检测 CSM 并在旧式启动/BIOS 模式下重新安装。

    b.  步骤 5 中，还是在与主启动磁盘 Diskpart.exe 选择，运行"转换 GPT"

      - 插入安装媒体上，重新启动，并通过安装程序。 如果遇到类似的文本的错误消息"不能安装到所选设备"或"磁盘格式不受支持"然后启动设备检测 CSM 和尝试启动到旧版启动 MBR 方法。

      - 或者，按照步骤手动配置 UEFI 启动方法的 GPT 磁盘。 看一下[Recommended UEFI-Based 磁盘分区配置](https://technet.microsoft.com/library/dd744301)然后运行 setup.exe 以第三分区为目标。

8. Windows 7 安装对系统和运行 （可能需要最新版本的修补程序） 后再升级到 Windows 10。

9. 一次安装 Windows 10 和修补，测试禁用 CSM，以及使用与制造商联系，以启用此系统上可用的安全选项。

    > [!NOTE]
    > 在某些情况下，固件都有特定于 UEFI 的启动选项。 例如，选择） 启动选项或 b) UEFI 启动选项。

## <a name="related-resources"></a>相关资源

[建议使用基于 UEFI 的磁盘分区配置](https://technet.microsoft.com/library/dd744301)
