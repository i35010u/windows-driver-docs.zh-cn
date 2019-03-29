---
title: MITT 入门
description: 若要运行 MITT 测试，必须在新的 MITT 板上安装 MITT 固件。 以下步骤介绍如何更新 MITT 固件和准备主机计算机上的运行 MITT 测试。
ms.assetid: 4467B82F-7B06-430B-A0CB-A6825045E5F4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb0f35e136ca13e608bbb3c25ae2975cfbe5a309
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563327"
---
# <a name="get-started-with-mitt"></a>MITT 入门


**上次更新时间**

-   2015 年 1 月

**适用于：**

-   Windows 8.1

若要运行 MITT 测试，必须在新的 MITT 板上安装 MITT 固件。 以下步骤介绍如何更新 MITT 固件和准备主机计算机上的运行 MITT 测试。

## <a name="before-you-begin"></a>开始之前...


-   [下载 MITT 软件包](https://msdn.microsoft.com/library/windows/hardware/dn919810)。
-   [购买硬件使用 MITT](https://msdn.microsoft.com/library/windows/hardware/dn919811)
-   了解如何使用提升的特权运行 Windows 命令行界面。 测试工具的安装需要提升的命令窗口。 为该窗口中，您可以打开命令提示符窗口使用**以管理员身份运行**选项。

## <a name="computer-setup-for-running-mitt-tests"></a>运行 MITT 测试的计算机设置


若要运行 MITT 测试，您需要将作为主机和待测系统 (SUT) 运行的计算机。

-   计算机必须运行 Windows 8.1 版本的操作系统。
-   计算机必须安装了 MITT 软件程序包。
-   计算机必须作为单独的计算机上运行的内核调试程序的目标连接。 有关如何获取 Windbg 的详细信息，请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063.aspx)。
    **请注意**  Windbg 可作为独立工具集进行安装。

     

-   ![适用于 windows phone](images/Phone.png)

**请注意**  如果你 SUT 是手机，则主机 SUT，并且必须配置 MITT 板，此图中所示。

![mitt 计算机设置](images/mitt-computer-setup.jpg)

## <a name="install-wdtf-runtime-library"></a>安装 WDTF 运行时库


若要运行 MITT 测试，需要 Windows 驱动程序测试框架 (WDTF)。 在安装 Windows Driver Kit (WDK) 时，运行时自动安装。 完整的安装说明，请按照中所述的步骤[WDTF 运行时库](https://msdn.microsoft.com/library/windows/hardware/hh831856)。

**下载位置**:[WDK 和 WinDbg 下载](https://go.microsoft.com/fwlink/p/?LinkId=733614)

运行时已安装此处 %programfiles （x86） %\\Windows 工具包\\8.1\\测试\\运行时\\TAEF

待测试系统必须连接到内核调试程序。 调试工具已安装 WDK。 有关详细信息，请参阅[调试工具的 Windows （WinDbg、 KD、 CDB、 NTSD）](https://msdn.microsoft.com/library/windows/hardware/ff551063)并[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff558823)。

## <a name="install-mitt-firmware"></a>安装 MITT 固件


1.  连接到主机计算机上的 USB 2.0 端口 MITT 板。 我们建议你使用根集线器端口，并避免嵌入中心的域控制器。
2.  请确保已打开板电源开关 （旁边的音频插孔）。 电源 LED 应为在红色。
3.  在设备管理器中，找到设备节点。

    ![设备节点的 mitt](images/install-mitt.png)

4.  右键单击节点并选择**更新驱动程序软件...**.
5.  选择**浏览计算机以查找驱动程序软件**中**更新驱动程序软件**对话框。
6.  选择**让我在我的计算机上从设备驱动程序的列表中选取**。
7.  选择**显示所有设备**然后单击**下一步**中**从以下列表中选择你的设备类型**页。
8.  单击**从磁盘安装...** 上**选择你想要安装这个硬件的设备驱动程序**页。
9.  浏览到 MITT 安装目录 (Program Files\\MITT\\*&lt;体系结构&gt;* 或 Program Files (x86)\\MITT\\ *&lt;体系结构&gt;*) 中**从磁盘安装对话框**然后单击**Ok**。
10. 下**制造商**选择**Microsoft**。 下**模型**选择**USB MUTT 默认**从列表中单击**下一步**。
11. 单击**是**安装的驱动程序。 忽略该驱动程序有关的警告可能与硬件兼容。 关闭的最后一页。
12. 在命令提示符中从 Program Files\\MITT\\*&lt;体系结构&gt;*，运行以下命令：

    **MuttUtil.exe -List**

    ![mitt 固件升级](images/mitt-setup1.png)

    上面的输出显示 WinUSB 加载作为看板的设备驱动程序。

13. 有两个单独的芯片需要 MITT 板上的固件。 对于此任务中，使用[MuttUtil](https://msdn.microsoft.com/library/windows/hardware/dn376874)。 运行此命令：

    **MuttUtil.exe – UpdateFirmware**

    如果使用 FPGA 开发板，EEPROM 可能最多 5 分钟的时间进行编程。 MuttUtil 比较 MuttUtil 中包含的固件版本与在板上的固件版本。 仅当 MuttUtil 具有更高版本的固件更新固件。

    ![mitt 固件升级](images/mitt-setup2.png)

    上面的输出显示了成功安装的第一个固件映像。

14. 运行**MuttUtil.exe – UpdateFirmware**再次为第二个芯片，第一次的固件更新完成后。 无法更新第二个芯片固件，只有在安装第一个芯片。

    ![mitt 固件升级](images/mitt-setup3.png)

    上面的输出显示了成功安装的第二个 MITT 固件映像。 请注意 MITT 板上的七个段。 你必须看到 000 X，其中 X 是 MITT 固件的当前版本。

**请注意**   **UpdateFirmware**选项不能还原 MITT 板上安装了工厂固件映像。

 

如果 MuttUtil 同时更新或安装固件，返回错误

-   检查 MITT 板上的电源开关上。 看板提供支持，如果拔出并将从看板的 USB 电缆和再次运行该命令。
-   如果命令成功，但七个段不会显示固件版本，通过按重置按钮或拔出并插入 USB 重新启动 MITT 板和电源线。 如果七个段仍未显示版本，请再次运行该命令。

## <a name="known-issues-and-workaround"></a>已知的问题和解决方法


-   不建议 MITT 直接连接到主计算机上的 xHCI 根集线器。 使用安装程序，测试可能会挂起随机。 作为一种解决方法，将添加一个电源的 USB 2.0 集线器 xHCI 端口和 MITT 板之间。

## <a name="related-topics"></a>相关主题
[使用多接口测试工具 (MITT) 进行测试](https://msdn.microsoft.com/library/windows/hardware/dn919874)  



