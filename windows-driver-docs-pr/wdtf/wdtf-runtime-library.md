---
title: WDTF 运行时库
description: WDTF 运行时库，它包含的工具以及如何安装的说明。
keywords:
- WDTF
- Windows 驱动程序测试框架
- WDTF 运行时
- 安装 WDTF
- 驱动程序测试
ms.date: 08/14/2018
ms.localizationpriority: medium
ms.openlocfilehash: e0d3456068a930d2ab8f3859709d1e45e0884c86
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136114"
---
# <a name="the-wdtf-runtime-library"></a>WDTF 运行时库

可用 WDTF 运行时库，则作为 Windows 驱动程序工具包 (WDK) 的一部分。 在安装 WDK 时，您还会安装 Windows 驱动程序测试框架 (WDTF)。 WDK 以及安装的模板和用于测试和开发的示例文件。 需要为你想要对运行 WDTF 基于测试任何系统上安装 WDTF 运行时库。 这包括在 WDK 中提供的测试和测试你编写使用 WDK 测试模板。

WDK 还包括可用于测试计算机上安装 WDTF 运行时的独立安装包 (*.msi)。 MSI 会执行以下操作：

- 将文件复制。

- 添加注册表项。

- 注册 WDTF 对象。

- 安装和卸载的日志文件。

WDTF 运行时库包括可帮助会审和运行测试工具。

|工具或命令的脚本的名称|描述|
|----|----|
|CheckWDTFInstall.cmd|验证 WDTF 正确安装。 运行此命令将创建文件 CheckWDTFInstall.log，其中包含所有已安装的 WDTF 组件的信息。|
|DisplayDeviceClass.vbs|显示当前的系统上存在的设备类信息。 显示类 GUID 和类友好名称。 如果尝试创建 /DQ 查找的设备的一类查询非常有用。|
|DisplayDeviceDataFields.cmd|显示当前的系统上存在的设备类信息。 显示类 GUID 和类友好名称。 如果尝试创建 /DQ 查找的设备的一类查询非常有用。|
|DisplayDevices.vbs|显示有关由 /DQ 参数，默认值表示每个设备的信息是在系统中的所有设备。 |
|DisplayDevicesWithWDTFilters.vbs|显示具有一个 WDTF 筛选器驱动程序在其上安装任何设备。 WDTF 具有三个筛选器驱动程序：EDT、 IOSPY 或按钮驱动程序。|
|DisplayDeviceTree.vbs|显示当前系统的设备树。|
|DisplaySystemDataFields.cmd|显示所有的系统命名空间和它们具有的字段。|

## <a name="how-to-install-the-wdtf-runtime-library"></a>如何安装 WDTF 运行时库

如果设置了测试计算机以进行部署时，测试计算机上安装 WDTF 运行时库。 按照中的说明[预配计算机，以使驱动程序部署和测试 （WDK 10 和 WDK 8.1）](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)

<!-- [Provision a computer for driver deployment and testing (WDK 8)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8) -->

您可以手动安装 WDTF 运行时库。

### <a name="installing-wdtf-on-a-test-computer-preferred-method"></a>（首选方法） 的测试计算机上安装 WDTF

1. 安装 Visual Studio，然后安装 WDK。

2. 配置用于测试的远程计算机。 在 Visual Studio 中，单击**驱动程序**菜单，依次指向**测试**，然后单击**配置计算机**。

### <a name="manually-installing-wdtf-on-a-test-computer-alternative-method"></a>（备选方法） 的测试计算机上手动安装 WDTF

1. 在用于开发的计算机上安装 Visual Studio 和 WDK。

2. WDTF 安装文件复制到测试计算机安装 WDK 其中的计算机中。 WDTF 安装文件 （*.msi 和 *.cab 文件） 位于 %programfiles%\Windows Kits\10\Testing\Runtimes 目录在开发系统上。 在测试计算机的体系结构匹配的目录中复制的所有文件。

3. 在测试计算机上打开命令提示符窗口，使用提升的权限 (**以管理员身份运行**) 并导航到包含 WDTF 安装文件的目录。 运行以下命令以安装 WDTF 之一。

    ```cmd
    msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi"
    ```

    -或者-

    ```cmd
    msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x86_en-us.msi"
    ```

下表描述了可用于的选项**msiexec**命令。

|选项|描述|
|----|----|
|**/l*** *filename*|将所有消息和错误都写入到文件中，*文件名*。|
|**WDTFDIR=**_CustomInstallationDirectory_|WDTF 运行时指定目标目录。 默认值**WDTFDir**是 %programfiles%\Windows Kits\10\Testing\Runtimes\WDTF|
|**WDTF_SKIP_MACHINE_CONFIG=[1 \| 2]**|指定**1**要跳过设置 cscript.exe 作为默认的脚本引擎。 指定**2**要跳过启用 AC 和 DC RTC 唤醒。|
|**/?**|显示有关 msiexec.exe 选项的帮助。|

### <a name="example"></a>示例

```cmd
msiexec /i "Windows Driver Testing Framework (WDTF) Runtime Libraries-x64_en-us.msi" /l* WDTFInstall.log WDTFDir=c:\wdtf WDTF_SKIP_MACHINE_CONFIG=1
```

## <a name="how-to-determine-if-the-wdtf-runtime-library-is-installed-on-a-compute"></a>如何确定是否在计算机上安装 WDTF 运行时库

你可以验证 WDTF 正确安装，可以通过在测试计算机上运行的命令脚本。 运行此命令将创建文件 CheckWDTFInstall.log，其中包含所有已安装的 WDTF 组件的信息。

1. 打开命令提示符窗口在测试计算机上。

2. 运行 `%WDTFDir%\Tools\CheckWDTFInstall.cmd`。

3. 打开日志文件 CheckWDTFInstall.log 并检查结果。

## <a name="how-to-uninstall-the-wdtf-runtime-library"></a>如何卸载 WDTF 运行时库

当您设置测试计算机以进行部署，以下说明[预配计算机，以使驱动程序部署和测试 (WDK 10)](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)，WDTF 运行时库安装在目标计算机上。

可以通过删除预配目标计算机中删除 WDTF 运行时库。 有关详细信息，请参阅[删除从目标计算机预配](https://docs.microsoft.com/windows-hardware/drivers/develop/what-happens-when-you-provision-a-computer--wdk-8-1-#span-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanspan-idremovingprovisioningfromthetargetcomputerspanremoving-provisioning-from-the-target-computer)。

你可以手动卸载 WDTF 运行时库。

## <a name="manually-uninstalling-wdtf-on-a-test-computer"></a>在测试计算机上中手动卸载 WDTF

1. 在测试计算机上转到**设置**，然后单击**应用**。

2. 在中**程序和功能**，找到 Windows 驱动程序测试框架 (WDTF) 运行时库中，右键单击并选择**卸载**。
