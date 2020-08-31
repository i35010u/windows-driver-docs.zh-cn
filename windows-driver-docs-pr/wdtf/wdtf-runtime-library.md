---
title: WDTF 运行时库
description: WDTF 运行时库的说明、它包含的工具以及如何安装。
keywords:
- WDTF
- Windows 驱动程序测试框架
- WDTF 运行时
- 安装 WDTF
- 驱动程序测试
ms.date: 08/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f67cfa32db5233b8aad54d9d79754ae4740dda5
ms.sourcegitcommit: 7a7e61b4147a4aa86bf820fd0b0c7681fe17e544
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89056939"
---
# <a name="the-wdtf-runtime-library"></a>WDTF 运行时库

WDTF 运行时库作为 Windows 驱动程序工具包的一部分提供 (WDK) 。 安装 WDK 时，还 (WDTF) 安装 Windows 驱动程序测试框架。 用于测试和开发的模板和示例文件与 WDK 一起安装。 需要在要运行基于 WDTF 的测试的任何系统上安装 WDTF 运行时库。 这包括 WDK 中提供的测试，以及使用 WDK 测试模板编写的测试。

WDK 还包含单独的安装包 ( * .msi) ，可用于在测试计算机上安装 WDTF 运行时。 MSI 执行以下操作：

- 复制文件。

- 添加注册表项。

- 注册 WDTF 对象。

- 安装和卸载日志文件。

WDTF 运行时库包含可帮助您会审和运行测试的工具。

|工具或命令脚本的名称|说明|
|----|----|
|CheckWDTFInstall|验证是否已正确安装 WDTF。 运行此命令将创建文件 CheckWDTFInstall，该文件包含有关所有已安装的 WDTF 组件的信息。|
|DisplayDeviceClass|显示当前系统上存在的设备类信息。 显示类 GUID 和类友好名称。 尝试创建查找某些设备类的/DQ 查询时非常有用。|
|DisplayDeviceDataFields|显示当前系统上存在的设备类信息。 显示类 GUID 和类友好名称。 尝试创建查找某些设备类的/DQ 查询时非常有用。|
|DisplayDevices|显示/DQ 参数表示的每个设备的相关信息，默认值为系统中的所有设备。 |
|DisplayDevicesWithWDTFilters|显示安装有其中一个 WDTF 筛选器驱动程序的任何设备。 WDTF 有三个筛选器驱动程序： EDT、IOSPY 或按钮驱动程序。|
|DisplayDeviceTree|显示当前系统的设备树。|
|DisplaySystemDataFields|显示所有系统命名空间及其包含的字段。|

## <a name="how-to-install-the-wdtf-runtime-library"></a>如何安装 WDTF 运行时库

设置测试计算机以进行部署时，会在测试计算机上安装 WDTF 运行时库。 按照[为驱动程序部署设置计算机和测试 (wdk 10 和 WDK 8.1) ](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)中的说明进行操作

<!-- [Provision a computer for driver deployment and testing (WDK 8)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8) -->

还可以手动安装 WDTF 运行时库。

### <a name="installing-wdtf-on-a-test-computer-preferred-method"></a>在测试计算机上安装 WDTF (首选方法) 

1. 安装 Visual Studio，然后安装 WDK。

2. 配置远程计算机以进行测试。 在 Visual Studio 中，选择 " **驱动程序** " 菜单，指向 " **测试**"，然后选择 " **配置计算机**"。

### <a name="manually-installing-wdtf-on-a-test-computer-alternative-method"></a>在测试计算机上手动安装 WDTF (备用方法) 

1. 在用于开发的计算机上安装 Visual Studio 和 WDK。

2. 将 WDTF 安装文件从安装了 WDK 的计算机复制到测试计算机。 WDTF 安装文件 ( * .msi 和 * .cab 文件) 位于开发系统上的%programfiles%\Windows Kits\10\Testing\Runtimes 目录中。 将目录中的所有文件复制到与测试计算机的体系结构相匹配的目录中。

3. 在测试计算机上，使用提升的权限打开命令提示符窗口 (**以管理员身份运行**) 并导航到包含 WDTF 安装文件的目录。 运行以下命令之一以安装 WDTF。

    ```cmd
    msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi"
    ```

    -或-

    ```cmd
    msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x86_en-us.msi"
    ```

下表介绍了可用于 **msiexec** 命令的选项。

|选项|说明|
|----|----|
|**/l** * *filename*|将所有消息和错误写入文件 *filename*。|
|**WDTFDIR =**_CustomInstallationDirectory_|指定 WDTF 运行时的目标目录。 默认 **WDTFDir** 为%programfiles%\Windows Kits\10\Testing\Runtimes\WDTF|
|**WDTF_SKIP_MACHINE_CONFIG = [1 \| 2]**|指定 **1** 以将 cscript.exe 设置为默认脚本引擎。 指定 **2** ，跳过启用 AC 和 DC RTC 唤醒。|
|**/?**|显示 msiexec.exe 选项的帮助。|

### <a name="example"></a>示例

```cmd
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi" /l* WDTFInstall.log WDTFDir=c:\wdtf WDTF_SKIP_MACHINE_CONFIG=1
```

## <a name="how-to-determine-if-the-wdtf-runtime-library-is-installed-on-a-compute"></a>如何确定计算上是否安装了 WDTF 运行时库

可以通过在测试计算机上运行命令脚本来验证是否已正确安装 WDTF。 运行此命令将创建文件 CheckWDTFInstall，该文件包含有关所有已安装的 WDTF 组件的信息。

1. 在测试计算机上打开 "命令提示符" 窗口。

2. 运行 `%WDTFDir%\Tools\CheckWDTFInstall.cmd`。

3. 打开日志文件 "CheckWDTFInstall" 并检查结果。

## <a name="how-to-uninstall-the-wdtf-runtime-library"></a>如何卸载 WDTF 运行时库

设置测试计算机以进行部署时，按照说明 [为驱动程序部署设置计算机并测试 (WDK 10) ](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)上，WDTF 运行时库安装在目标计算机上。

可以通过从目标计算机中删除预配来删除 WDTF 运行时库。 有关详细信息，请参阅 [从目标计算机中删除设置](https://docs.microsoft.com/windows-hardware/drivers/develop/what-happens-when-you-provision-a-computer--wdk-8-1-#span-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanremoving-provisioning-from-the-target-computer)。

还可以手动卸载 WDTF 运行时库。

## <a name="manually-uninstalling-wdtf-on-a-test-computer"></a>在测试计算机上手动卸载 WDTF

1. 在测试计算机上，中转到 " **设置** "，然后选择 " **应用**"。

2. 在 " **程序和功能**" 中，找到 Windows 驱动程序测试框架 (WDTF) 运行时库，选择并按住 (或右键单击) ，然后选择 " **卸载**"。
