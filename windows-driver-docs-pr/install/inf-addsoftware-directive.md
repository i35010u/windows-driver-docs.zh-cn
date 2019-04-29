---
title: INF AddSoftware 指令
description: AddSoftware 指令介绍独立软件的安装。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 19d093ba078d3dba4ecbf03694ec0e47f2803d3f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379465"
---
# <a name="inf-addsoftware-directive"></a>INF AddSoftware 指令

每个**AddSoftware**指令介绍独立软件的安装。  在的 INF 文件中使用此指令**SoftwareComponent**安装程序类。 软件组件的更多详细信息，请参阅[使用组件 INF 文件](using-a-component-inf-file.md)。  适用于 Windows 10 版本 1703年及更高版本支持此指令。

有效的安装类型取决于[目标平台](../develop/windows-10-editions-for-universal-drivers.md)。 例如，桌面支持 MSI 安装程序和 Exe 安装程序。  **注意**：在通用驱动程序支持类型 2 中，键入 1 是仅适用于桌面。

当软件组件 INF 文件指定了**AddSoftware**，系统队列设备安装之后安装软件。  就不能保证时，或将安装该软件。
如果被引用的软件无法安装，系统重试更新引用的软件组件时。

**AddSoftware**中使用指令[ **INF *DDInstall*。软件**](inf-ddinstall-software-section.md)部分。

```ini
[DDInstall.Software]
AddSoftware=SoftwareName,[flags],software-install-section
```

## <a name="entries"></a>条目

*SoftwareName*

指定要安装的软件的名称。  此名称唯一标识该软件。  在处理**AddSoftware**指令检查版本与安装具有相同名称的上一软件**AddSoftware**指令从任何驱动程序包。  我们建议作为开端 SoftwareName 与供应商名称，例如`ContosoControlPanel`。

*flags*

指定一个或多个 （或运算） 标志。

**0x00000000**  
**AddSoftware**指令处理只能一次。

**0x00000001**  
**AddSoftware**指令指定每个组件设备处理一次**AddSoftware**使用相同的唯一*SoftwareName*。

*software-install-section*

引用了一个 INF 编写器定义的部分，其中包含用于安装软件的信息。
    
## <a name="remarks"></a>备注

每个 INF 编写器创建的部分名称的 INF 文件中必须是唯一和必须遵从常规规则，用于定义的节名称。  有关这些规则的详细信息，请参阅[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

**AddSoftware**指令必须引用一个已命名*软件安装部分*INF 文件中的其他位置。  每个此类部分具有以下形式：

```ini
[software-install-section]

SoftwareType=type-code
[SoftwareBinary=path-to-binary]
[SoftwareArguments=argument[, argument] …]
[SoftwareVersion=w.x.y.z]
[SoftwareID=pfn://x.y.z]
```

**SoftwareType**项是必需的。  如果**SoftwareType**设置为 1， **SoftwareBinary**并**SoftwareVersion**也是必需的但自变量和标志是可选的。 如果**SoftwareType**设置为 2， **SoftwareID**是必需的并且是可选的标志。

使用安装任何软件**AddSoftware**必须以无提示方式 （或安静模式） 安装。 换而言之，没有用户界面可以向用户显示在安装过程中。

使用安装任何软件**AddSoftware**将**不**如果卸载虚拟软件组件设备或其父设备中卸载。 如果您的软件不是 UWP 应用 (即使用**AddSoftware** ，值为 1)，请确保用户可以轻松地卸载它而无需离开在注册表中的跟踪。 为此，请执行以下操作：

* 如果使用 MSI 安装程序，设置[添加/删除程序](https://msdn.microsoft.com/library/windows/desktop/aa368032)应用程序的 Windows 安装程序包中的条目。
* 如果您使用的自定义 EXE 安装全局的注册表文件状态 （而不是补充本地设备设置），使用[卸载注册表项](https://msdn.microsoft.com/library/windows/desktop/aa372105)。 

## <a name="software-install-section-entries-and-values"></a>软件安装节条目和值

**SoftwareType**=*type-code*

指定软件安装类型。

如果值为 1 指示关联的软件的 MSI 或 EXE 的二进制文件。  当设置此值时， **SoftwareBinary**项也是必需的。  Windows 10 s。 不支持的值为 1 从 Windows 10 1709年版开始，值为 2 表示关联的软件的 Microsoft Store 的链接。  仅为没有图形用户界面的特定于设备的软件使用的值为 1。  如果您有包含图形元素的特定于设备的应用程序，它应来自 Microsoft Store 中，并且驱动程序应引用它使用**SoftwareType** 2。

>[!NOTE]
>在使用类型 2 的 AddSoftware 指令，它不需要利用组件 INF。  指令可在任何 INF 成功。  键入 1，一个 AddSoftware 指令但是，必须使用从组件 INF。

不要使用 AddSoftware 将与设备无关的软件分发。 例如，不应与 AddSoftware 安装特定于 OEM PC 实用程序。
相反，使用以下选项之一来预安装 Windows 10 的 OEM 映像中的应用：

* 若要预安装 Win32 应用程序，启动到审核模式，再安装应用。 有关详细信息，请参阅[审核模式概述](https://docs.microsoft.com/windows-hardware/manufacture/desktop/audit-mode-overview)。
* 若要预安装的 Microsoft Store (UWP) 应用，请参阅[Preinstallable 适用于桌面设备应用](https://docs.microsoft.com/windows-hardware/customize/preinstall/preinstallable-apps-for-windows-10-desktop)。

有关配对的驱动程序有一个通用 Windows 平台 (UWP) 应用程序的信息，请参阅[配对使用通用 Windows 平台 (UWP) 应用程序的驱动程序](pairing-app-and-driver-versions.md)和[硬件支持应用程序 (HSA):适用于驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)。

**SoftwareBinary**=*filename*

指定可执行文件的路径。  系统会生成如下所示的命令行：

`MSI: msiexec /i "<SoftwareBinary>” ALLUSERS=1 /quiet /qn /promptrestart [<SoftwareArguments>]`

`EXE: <SoftwareBinary> [<SoftwareArguments>]`

如果使用此项，则必须添加可执行文件到 DriverStore 通过指定[INF CopyFiles 指令](inf-copyfiles-directive.md)与**DestinationDirs**值 13。

**SoftwareArguments**=*argument1[, argument2[, … argumentN]]*

指定要追加到命令行的特定于扩展插件参数。  可以指定系统只需传递到生成的命令行的命令行参数。  此外可以指定名为的特殊字符串*运行时上下文变量*。  当指定运行时上下文变量时，系统将其转换为特定于设备的值追加到生成的命令行之前。  您可以混合和匹配文本字符串的参数和运行时上下文变量。  支持的运行时上下文变量包括：

`<<DeviceInstanceID>>`

系统将上面的字符串替换设备实例 ID 的软件组件。

例如：

```ini
    [DDInstall.Software]
    AddSoftware=ContosoControlPanel,,Contoso_ControlPanel_Software

    [Contoso_ControlPanel_Software]
    SoftwareType=1
    SoftwareBinary=ContosoControlPanel.exe
    SoftwareArguments=<<DeviceInstanceID>>
    SoftwareVersion=1.0.0.0
```

上面的命令行中的示例结果如下所示：

`<DriverStorePath>\ContosoControlPanel.exe PCI\VEN_0000&DEV_0001&SUBSYS_00000000&REV_00\0123`

如果 SoftwareArguments 包含多个参数：

```ini
    SoftwareArguments=arg1,<<DeviceInstanceID>>,arg2
```

在上面的结果：

`<DriverStorePath>\ContosoControlPanel.exe arg1 PCI\VEN_0000&DEV_0001&SUBSYS_00000000&REV_00\0123 arg2`

**SoftwareVersion**=*w.x.y.z*

指定的软件版本。  每个值不应超过 65535。  当系统遇到重复**SoftwareName**，它会检查**SoftwareVersion**针对以前**SoftwareVersion**。  如果超出该时间后，Windows 将运行的软件。

**SoftwareID**=*x.y.z*

指定 Microsoft Store 标识符和标识符类型。  目前，支持仅包系列名称 (PFN)。  使用 PFN 引用使用窗体的通用 Windows 平台 (UWP) 应用`pfn://<x.y.z>`。

<!--add link to related page in UWP docs once it is available-->

## <a name="see-also"></a>请参阅

* [使用组件 INF 文件](using-a-component-inf-file.md)。
* [INF DDInstall.Software 部分](inf-ddinstall-software-section.md)
* [INF AddComponent 指令](inf-addcomponent-directive.md)
* [配对的驱动程序有一个通用 Windows 平台 (UWP) 应用程序](pairing-app-and-driver-versions.md)
* [硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
