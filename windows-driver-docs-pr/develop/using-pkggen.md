---
title: 在 Windows 10 移动版上安装驱动程序
description: 描述在 Windows 10 移动版上安装驱动程序的过程。
ms.date: 06/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a4910567ed8a23df6b4218341e28cd9243d2e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518070"
---
# <a name="installing-a-driver-on-windows-10-mobile"></a>在 Windows 10 移动版上安装驱动程序

若要在 Windows 10 移动版上安装驱动程序，请使用 .spkg 文件。 .spkg（“包文件”）是一个包含驱动程序包的独立模块。

WDK 10 包括 PkgGen，后者是一个生成包文件的工具。 使用以下过程在生成驱动程序时在 Visual Studio 中运行 PkgGen。

**使用 PkgGen 生成包文件**

1.  右键单击驱动程序项目，然后选择“添加”-&gt;“新项目”。 接下来，在“Visual C++”-&gt;“Windows 驱动程序”下，选择“程序包清单”。 单击**添加**。
2.  Visual Studio 会将名为 Package.pkg.xml 的文件添加到你的驱动程序项目。 你可以右键单击该文件，然后选择属性来确认项目类型是 **PkgGen**。 （在同一个属性页中，如果你稍后决定要生成此驱动程序项目且不生成包文件，可以将“从生成中排除”设置为“是”。）单击“确定” 。
3.  右键单击该驱动程序项目，然后选择“属性”。 在“配置属性”下打开 PackageGen 节点，将“版本”更改为你喜欢的任意值。
4.  保存工作数据，并以管理员身份重启 Visual Studio。
5.  生成驱动程序。 Visual Studio 链接所需库并生成 .cat 文件、.inf 文件、驱动程序二进制文件和 .spkg 文件。

若要查看包文件的内容，将 .cab 后缀追加到文件名后面，然后在 Windows 资源管理器中打开此 cab 文件。

若要了解有关在 Visual Studio 外部运行 PkgGen 的信息，请参阅[创建移动程序包](https://msdn.microsoft.com/Library/Windows/Hardware/Dn756642)。

若要安装移动驱动程序包（.spkg 文件），你有两个选择。

-   如果你是在目标系统上更新现有包或将新包添加到目标系统，请使用 IUTool.exe 安装 .spkg 驱动程序包。
-   如果你要将包合并为一个移动 OS 映像，请使用 ImgGen 将 .spkg 驱动程序包添加到随后可被刷入移动设备的完整闪存更新 (FFU) 映像。

**使用 IUTool 将移动驱动程序包 (.spkg) 添加到正在运行的设备**

1.  IUTool.exe 位于 WDK 10 的 \\tools\\bin\\*&lt;architecture&gt;* 子目录中。

    将移动设备附加到电脑。 然后，从提升的命令提示符发出以下命令：

       ```cpp
       IUTool -p MyKmdfDriver.spkg
       ```

2.  有关详细信息，请参阅[将驱动程序添加到测试映像](https://msdn.microsoft.com/Library/Windows/Hardware/Mt131832)。

**使用 ImgGen 将移动驱动程序包 (.spkg) 添加到移动 OS 映像 (.ffu)**

1.  安装 Visual Studio 后，在“开始”屏幕上，单击“Visual Studio 2015”文件夹。 右键单击“适用于 VS2015 的开发人员命令提示”，然后选择“以管理员身份运行”。

## <a name="span-idflashingamobileosimageffuspanspan-idflashingamobileosimageffuspanflashing-a-mobile-os-image-ffu"></a><span id="flashing_a_mobile_os_image__.ffu_"></span><span id="FLASHING_A_MOBILE_OS_IMAGE__.FFU_"></span>刷写移动 OS 映像 (.ffu)

若要将映像刷入设备，请使用 Microsoft 提供的 FFUTool，或开发自定义的 OEM 刷写工具。
