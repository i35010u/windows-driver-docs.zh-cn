---
title: CFU 虚拟 HID 设备固件更新模拟
description: 提供虚拟 HID 设备上模拟固件更新的演练。
ms.date: 10/01/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 4e8922a595507f6d9a99cb12bc8fec85541beb24
ms.sourcegitcommit: eefc6ae6d9621d0735b3c63e718ee5838d57a6bc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92886333"
---
# <a name="cfu-virtual-hid-device-firmware-update-simulation"></a>CFU 虚拟 HID 设备固件更新模拟

本主题提供了虚拟 HID 设备上模拟固件更新的演练。

## <a name="build-and-install-the-cfu-virtual-hid-device-sample"></a>生成并安装 CFU 虚拟 HID 设备示例

1. 安装 Visual Studio 2019 和 Windows 驱动程序工具包 (WDK) ，如 [下载 Windows 驱动程序工具包 (wdk) ](/windows-hardware/drivers/download-the-wdk)所述。

1. 将 Microsoft CFU 存储库克隆到本地存储库目录

    `git clone https://github.com/microsoft/CFU.git`

1. 在本地 CFU 存储库目录中，在命令提示符下运行以下 git 命令，以获取用于生成示例所需的驱动程序模块框架 (DMF) 子模块：

    `git submodule init`

    `git submodule update`

1. 在 Visual Studio 中生成 CfuVirtualHid 设备解决方案

    1. 导航到开发系统上的 CfuVirtualHid 文件所在的位置。 例如：

        `C:\<your_repo_folder>\CFU\Host\CFUFirmwareSimulation\CfuVirtualHid.sln`

    1. 在 Visual Studio 中打开 CfuVirtualHid 文件。

    1. 在 " **生成** " 菜单中，选择 " **生成解决方案** "。 应会看到输出文本，指示已成功生成解决方案：

        ![CfuVirtualHid 生成成功](images/cfuvirtualhid-build-succeeded.png)

1. 安装 CfuVirtualHid 设备和驱动程序

    1. 导航到开发系统上的 cfuvirtualhid 文件所在的位置。 例如：

        `C:\<your_repo_folder>\CFU\Host\CFUFirmwareSimulation\x64\Debug\CfuVirtualHid`

    1. 在管理命令提示符下，运行以下命令：

        ```console
        devcon.exe install cfuvirtualhid.inf HID\CFU_VIRTUAL_DEVICE
        ```

        应会看到表明虚拟设备已成功安装的输出文本：

        ![CfuVirtualHid 设备安装成功](images/cfuvirtualhid-device-install-succeeded.png)

1. 在 " **控制面板** " 中，打开 **设备管理器** ，选择 " **视图** " 菜单，然后选择 " **按类型显示设备** " 菜单项。

1. 在 "设备" 列表中，展开 " **固件** " 节点，然后选择 **CfuVirtualHid 设备** ，如下所示：

     ![已选择 CfuVirtualHid 设备](images/cfuvirtualhid-device-selected.png)

1. 右键单击 **CfuVirtualHid 设备** 打开上下文菜单，然后单击 " **属性** " 菜单项以打开 " **CfuVirtualHid 设备属性** " 对话框窗口。

1. 在 " **CfuVirtualHid 设备属性** " 对话框窗口中选择 " **详细信息** " 选项卡，然后在 " **属性** " 下拉列表中选择 " **硬件 id** "。

    你应在 " **值** " 列表框中看到 **HID \ CFU_VIRTUAL_DEVICE** ，如下所示：

    !["值" 列表框中的 HID \ CFU_VIRTUAL_DEVICE](images/cfuvirtualhid-device-selected.png)

1. 在 " **设备管理器** " 菜单中，选择 " **视图** " 菜单，然后选择 " **按连接显示设备** " 菜单项。

    ![CfuVirtualHid 按连接查看设备](images/cfuvirtualhid-view-devices-by-connection.png)

1. 导航到 " **CfuVirtualHid" 设备** 并展开 **"CfuVirtualHid" 设备** 节点，展开 " **虚拟 HID 框架 (VHF") hid 设备** "节点，然后选择" **符合 HID 标准的设备** 列表 "项，如下所示：

    ![与 HID 兼容的设备列表项](images/hid-compliant-device-list-item.png)

1. 右键单击与 **HID 兼容的设备** 以打开上下文菜单，然后单击 " **属性** " 菜单项以打开 " **符合 HID 标准的设备属性** " 对话框窗口。

1. 在 " **符合 HID 标准的设备属性** " 对话框窗口中选择 " **详细信息** " 选项卡，然后在 **属性** 下拉列表中选择 " **硬件 id** "。

    你应在 " **值** " 列表框中看到 **HID \ VID_045E&UP： FA00_U： 00F5** ，如下所示：

    ![值列表中的 HID VID 设备](images/hid-vid-045e-up-fa00-u-00f5-device-list-item.png)

## <a name="install-a-firmware-update-for-the-cfu-virtual-hid-device"></a>安装 CFU 虚拟 HID 设备的固件更新

本部分提供有关在 Visual Studio 2019 中构建的示例 [**CfuVirtualHid 设备**](https://github.com/microsoft/CFU/tree/master/Host/CFUFirmwareSimulation) 设备上安装固件更新的示例，并使用 [**devcon.exe**](/windows-hardware/drivers/devtest/devcon) 命令行工具安装固件更新，如以上部分所述。

1. 导航到 .inf 文件的位置，以及目标设备的固件提供和负载 bin 文件。 例如：

    ![步骤 1](images/install-cfu-virtual-device-firmware-update-1.png)

1. 在文本编辑器中，打开固件更新 INF 文件。 在此示例中，我们将使用 [CFU inf 配置](cfu-inf-configuration.md)中所述的 *CfuVirtualHidDeviceFwUpdate* 文件。

1. 在固件更新 INF 文件中，转到 `[Standard.NTamd64]` 部分，并验证 **HID \ VID_045E&UP： FA00_U： 00F5** 设备的以下信息：

    ```inf
    [Standard.NTamd64]
    %CfuVirtualHidDeviceFwUpdate.DeviceDesc%=CfuVirtualHidDeviceFwUpdate, HID\VID_045E&UP:FA00_U:00F5 ; HardwareID for VirtualHidDevice MCU

    [CfuVirtualHidDeviceFwUpdate.NT]
    Include            = HidCfu.inf
    Needs              = HidCfu.NT
    CopyFiles          = CfuVirtualHidDeviceFwUpdate.CopyFiles

    [CfuVirtualHidDeviceFwUpdate.NT.Wdf]
    Include            = HidCfu.inf
    Needs              = HidCfu.NT.Wdf
    ```

1. 在管理命令提示符下，运行以下命令：

    `pnputil /add-driver CfuVirtualHidDeviceFwUpdate.inf /install`

    此命令将返回 PnP 实用工具输出。 例如：

    ![pnp 实用工具输出](images/install-cfu-virtual-device-firmware-update-2.png)

1. 在 **设备管理器** 中，导航到 **CfuVirtualHid 设备** 节点，然后展开节点以验证是否已安装 **CfuVirtualHidDevice 固件更新** ，如下所示：

    ![已安装 cfu 虚拟 hid 设备固件更新](images/install-cfu-virtual-device-firmware-update-3.png)

1. 选择 " **CfuVirtualHidDevice 固件更新** " 节点，然后打开 " **CfuVirtualHidDevice 固件更新属性** " 窗口，如下所示：

    ![cfu 虚拟 hid 设备固件更新属性窗口](images/install-cfu-virtual-device-firmware-update-4.png)

1. 在 " **CfuVirtualHidDevice 固件更新属性** " 窗口中，选择 **"详细信息** " 选项卡，然后在 **属性** 下拉列表中选择 " **硬件 id** "，如下所示：

    ![属性下拉列表中的硬件 id](images/install-cfu-virtual-device-firmware-update-5.png)

1. 验证 **HID \ VID_045E&UP： FA00_U： 00F5** 设备是否出现在 **CfuVirtualHidDevice 固件更新** 的 " **硬件 id** " **值** 中。

    ![值列表中的硬件 id](images/install-cfu-virtual-device-firmware-update-6.png)

1. 使用 **TraceView** 应用程序查看 CFU 虚拟 HID 设备安装的日志消息信息。 例如：

    ![traceview 日志消息信息](images/install-cfu-virtual-device-firmware-update-7.png)
