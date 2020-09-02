---
title: MITT 入门
description: 若要运行 MITT 测试，必须在新的 MITT 板上安装 MITT 固件。 以下步骤介绍了如何更新 MITT 固件并准备好主机以运行 MITT 测试。
ms.assetid: 4467B82F-7B06-430B-A0CB-A6825045E5F4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9175cfb211836aa8ba59d7625329d4ac284ea677
ms.sourcegitcommit: c766ab74e32eb44795cbbd1a4f352d3a6a9adc14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89389549"
---
# <a name="get-started-with-mitt"></a>MITT 入门


**上次更新时间**

-   2015年1月

**适用于：**

-   Windows 8.1

若要运行 MITT 测试，必须在新的 MITT 板上安装 MITT 固件。 以下步骤介绍了如何更新 MITT 固件并准备好主机以运行 MITT 测试。

## <a name="before-you-begin"></a>开始之前 .。。


-   [下载 MITT](/previous-versions/dn919810(v=vs.85))软件包。
-   [使用 MITT 购买硬件](./multi-interface-test-tool--mitt--.md)
-   了解如何通过提升的权限运行 Windows 命令行界面。 安装测试工具需要提升的命令窗口。 对于该窗口，您可以使用 "以 **管理员身份运行** " 选项打开命令提示符窗口。

## <a name="computer-setup-for-running-mitt-tests"></a>运行 MITT 测试的计算机设置


若要运行 MITT 测试，需要一台计算机，该计算机将作为 (SUT) 测试的主机和系统运行。

-   计算机必须运行 Windows 8.1 版本的操作系统。
-   计算机必须安装 MITT 软件包。
-   计算机必须作为目标连接到在单独计算机上运行的内核调试器。 有关如何获取 Windbg 的详细信息，请参阅 [Windows 调试](../debugger/index.md)。
    **注意**   Windbg 可以作为独立的工具集进行安装。

     

-   ![适用于 windows phone](images/Phone.png)

**注意**   如果你的 SUT 是一部手机，则必须配置主计算机、SUT 和 MITT 板，如图所示。

![mitt 计算机设置](images/mitt-computer-setup.jpg)

## <a name="install-wdtf-runtime-library"></a>安装 WDTF 运行时库


若要运行 MITT 测试，需要 (WDTF) 的 Windows 驱动程序测试框架。 在 (WDK) 上安装 Windows 驱动程序工具包时，将自动安装运行时。 有关完整的安装说明，请按照 [WDTF 运行时库](/windows-hardware/drivers/ddi/index)中所述的步骤进行操作。

**下载位置**： [WDK 和 WinDbg 下载](https://go.microsoft.com/fwlink/p/?LinkId=733614)

运行时安装在此处% ProgramFiles (x86) % \\ Windows 工具包 \\ 8.1 \\ 测试 \\ 运行时 \\ TAEF

要测试的系统必须连接到内核调试器。 调试工具随 WDK 一起安装。 有关详细信息，请参阅 [Windows 调试工具 (WinDbg、KD、CDB、NTSD) ](../debugger/index.md) 和 [Windows 调试](../debugger/symbols.md)。

## <a name="install-mitt-firmware"></a>安装 MITT 固件


1.  将 MITT 板连接到主计算机上的 USB 2.0 端口。 建议使用根集线器端口，并避免使用嵌入的集线器的控制器。
2.  请确保 "音频插孔" 旁边的 "板 (") 处于打开状态。 红色电源 LED 应亮起。
3.  在设备管理器中，找到 "设备" 节点。

    ![mitt 的设备节点](images/install-mitt.png)

4.  右键单击该节点，然后选择 " **更新驱动程序软件 ...**"。
5.  在 "**更新驱动程序软件**" 对话框中选择 "**浏览计算机以查找驱动程序软件**"。
6.  选择 **"让我从计算机上的设备驱动程序列表中**选择"。
7.  选择 "**显示所有设备**"，然后在 "**从以下列表中选择设备的类型**" 页中单击 "**下一步**"。
8.  单击 "**选择要为此硬件安装的设备驱动程序**" 页上的 "**已安装磁盘 ...** "。
9.  在 "从磁盘安装" 对话框中，浏览到 MITT 安装目录 (Program files \\ MITT \\ * &lt; &gt; 体系结构*或 program files (x86) \\ MITT \\ * &lt; 体系结构 &gt; *) ，然后单击 **"确定"**。 **Install From Disk dialog**
10. 在 " **制造商** " 下，选择 " **Microsoft**"。 在 " **模型** " 下，从列表中选择 " **MUTT** "，并单击 " **下一步**"
11. 单击 **"是"** 并安装驱动程序。 忽略有关驱动程序的警告可能与硬件兼容。 关闭最后一页。
12. 在命令提示符下，从 Program Files \\ MITT \\ * &lt; 体系结构 &gt; *运行以下命令：

    **MuttUtil.exe-列表**

    ![mitt 固件升级](images/mitt-setup1.png)

    前面的输出显示，WinUSB 已加载为板的设备驱动程序。

13. 有两个单独的芯片需要 MITT 板上的固件。 对于此任务，请使用 [MuttUtil](../usbcon/index.md)。 运行以下命令：

    **MuttUtil.exe – UpdateFirmware**

    如果你使用的是 FPGA 开发板，则 EEPROM 最多需要5分钟才能完成编程。 MuttUtil 将板上的固件版本与 MuttUtil 中包含的固件版本进行比较。 仅当 MuttUtil 具有更高版本的固件时才更新固件。

    ![mitt 固件升级](images/mitt-setup2.png)

    前面的输出显示成功安装第一个固件映像。

14. 在第一个固件更新完成后，为第二个芯片再次运行 **MuttUtil.exe-UpdateFirmware** 。 在安装第一个芯片之前，无法更新第二个芯片的固件。

    ![mitt 固件升级](images/mitt-setup3.png)

    前面的输出显示已成功安装第二个 MITT 固件映像。 请注意 MITT 板上的七段。 必须查看1,000 倍，其中 X 是当前版本的 MITT 固件。

**注意**   **UpdateFirmware**选项无法还原 MITT 板上安装的工厂固件映像。

 

如果 MuttUtil 在更新或安装固件时返回错误，

-   检查 MITT 板上的电源开关是否已打开。 如果该板已通电，请拔下并拔下板上的 USB 电缆，然后再次运行该命令。
-   如果命令成功但七个段未显示固件版本，请按 "重置" 按钮重启 MITT 板，或者拔下并插入 USB 和电源线。 如果七段仍未显示版本，请再次运行该命令。

## <a name="known-issues-and-workaround"></a>已知问题和解决方法


-   建议不要将 MITT 直接连接到主计算机上的 xHCI 根集线器。 此安装程序可能会随机挂起测试。 解决方法是在 xHCI 端口和 MITT 板之间添加已通电的 USB 2.0 集线器。

## <a name="related-topics"></a>相关主题
[通过多接口测试工具进行测试 (MITT) ](./testing-with-multi-interface-test-tool--mitt-.md)