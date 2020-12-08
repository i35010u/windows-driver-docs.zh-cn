---
title: 如何安装 Windows 安装程序和启动所需的测试签名的驱动程序
description: 描述如何在运行 Windows Server 的计算机上或在 Windows 安装程序
ms.date: 10/06/2020
ms.openlocfilehash: 66c9370cbe2475a3cbc4d54ec841a853a943bc62
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828653"
---
# <a name="how-to-install-a-test-signed-driver-required-for-windows-setup-and-boot"></a>如何安装 Windows 安装程序和启动所需的测试签名的驱动程序

本页介绍如何在运行 Windows Server 2019 (或 Windows Server 2016) 的计算机上或在 Windows 安装程序后首次启动的计算机上安装测试签名的驱动程序。 只应在测试环境中使用测试签名的驱动程序。

有关详细信息，请参阅 [测试签名简介](introduction-to-test-signing.md)。

在开始之前，请确保具备以下条件：
* 用于 ADK 的[Windows 评估和部署工具包 (adk) ](/windows-hardware/get-started/adk-install)和 windows PE 外接程序
* Windows Server 2019 或2016安装媒体 ISO 文件

## <a name="creating-the-iso-file"></a>创建 ISO 文件

使用以下步骤创建 ISO 文件并从中安装 Windows：
1. 在 "ADK 开始菜单" 选项中，选择 " **部署和映像工具环境**"，右键单击，然后选择 " **以管理员身份运行**"。
2. 运行 **copype.cmd** 以创建 Windows PE 文件的工作副本： `copype amd64 C:\WinPE_amd64`
3. 启用 **testsigning**。 在非 UEFI (旧) 计算机上，使用：

```cmd
cd C:\WinPE_amd64\media\Boot
bcdedit /store .\BCD /enum all
bcdedit /store .\BCD /set {default} testsigning on
```

在 UEFI 平台上，使用：

```cmd
cd C:\WinPE_amd64\media\EFI\Microsoft\Boot
bcdedit /store .\BCD /enum all
bcdedit /store .\BCD /set {default} testsigning on
```

4. 若要验证 `testsigning Yes` 现在是否在 Windows 启动加载程序下显示了 {default} 标识符，请 `bcdedit /store .\BCD /enum all` 再次运行。

5.  将 Windows Server 2016 安装媒体 ISO 文件装载到驱动器（例如）， `G` 并手动将 "源" 文件夹下的所有文件（例如 `G:\sources` ）复制到 WinPE 系统文件的 "源" 文件夹，例如 `C:\WinPE_amd64\media\sources` 。

> [!NOTE]
> 不要覆盖 `boot.wim` 文件夹中的现有文件 `C:\WinPE_amd64\media\sources` 。 稍后我们将使用原始 WinPE 环境。

现在，我们有了所有文件，包括 WinPE 和 Windows Server 2016。

6. （可选）将测试签名的驱动程序复制到该文件夹 `C:\WinPE_amd64\media` 。 复制的文件可能包含驱动程序的 .cat、.cer、.inf 和 .sys 文件。
使用以下命令将测试签名驱动程序导入到 WIM 文件：

```cmd
Dism /Get-WimInfo /wimfile:C:\WinPE_amd64\media\sources\install.wim
Dism /Mount-Image /imagefile:C:\WinPE_amd64\media\sources\install.wim /index:4 /mountdir:C:\WinPE_amd64\mount
Dism /image:C:\WinPE_amd64\mount /Add-Driver /driver:C:\WinPE_amd64\media\DriverSample
Dism /unmount-image /mountdir:C:\WinPE_amd64\mount /commit
```

7.  创建新的 ISO 文件： `Makewinpemedia /iso C:\winpe_amd64 C:\WS2016_amd64.iso` 。 尽管 ISO 文件中的默认应用程序是 cmd.exe，但你将手动启动 setup.exe 以在安装后配置启动设置。  

8. 从安装 Windows Server 2016 `WS2016_amd64.iso` 。 （可选）自定义安装源以导入更多驱动程序。

## <a name="installing-the-driver"></a>安装驱动程序

使用以下步骤安装该驱动程序：

1. 在测试计算机上关闭 **安全启动** ，然后启动 WinPE 系统。
2. 使用 ISO 文件启动计算机后，将显示命令提示符。
3. 若要使用装载的 ISO 文件来识别驱动器号，请使用 `diskpart` ，然后使用 `list volume` 。 查找 **类型** 为的卷 `DVD-ROM` 。 键入 `exit`。
4. 导航到 ISO 驱动器并切换到驱动程序示例目录，例如 `D:\DriverSample` 。
5. 使用以下命令安装测试驱动程序：
```cmd
certmgr.exe -add DriverSample.cer -s -r localmachine root
certmgr.exe -add DriverSample.cer -s -r localmachine trustedpublisher
devcon.exe install DriverSample.inf Root\DriverSample
```
6. 还可以通过查看日志来确认安装 `setupapi.dev` 。
7. 运行 `setup.exe /NoReboot` ，例如来自 `D:\sources` 。
8. 安装完成后，将显示一条消息，指示可以关闭安装应用程序。 退出应用程序以返回到 WinPE 命令提示符。
9. 键入 `diskpart`。 确定操作系统启动分区和该启动分区的驱动器号 (仅 FAT32 分区，大小约为 100MB) 
10. 导航到启动分区驱动器并将目录切换到 BCD 文件的位置，例如 `E:\EFI\Microsoft\Boot` 。
11. 打开 **testsigning**： `bcdedit /store BCD /set {default} testsigning on` 并重新启动计算机。
12. 若要确认计算机处于测试模式，请在桌面的右下角查找 **测试模式** 水印。

计算机必须处于测试模式才能加载测试签名的驱动程序。 如果有需要测试签名驱动程序的启动设备，则必须将测试签名的驱动程序导入到 WIM 文件 (使用上述的可选 Dism 步骤) 以避免在以后使用 PnP。 如果关闭 **testsigning** 设置，计算机可能无法启动。
