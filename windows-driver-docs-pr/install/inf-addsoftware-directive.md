---
title: INF AddSoftware 指令
description: AddSoftware 指令介绍了独立软件的安装。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26de0aa0f35add9159a49f457fb76c9786b7dd56
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223275"
---
# <a name="inf-addsoftware-directive"></a>INF AddSoftware 指令

每个**AddSoftware**指令描述独立软件的安装。  在**SoftwareComponent**安装程序类的 INF 文件中使用此指令。 有关软件组件的详细信息，请参阅[使用组件 INF 文件](using-a-component-inf-file.md)。  Windows 10 版本1703及更高版本支持此指令。

有效的安装类型取决于[目标平台](../develop/windows-10-editions-for-universal-drivers.md)。 例如，桌面支持 MSI 安装程序和安装程序 Exe。  **注意**：通用驱动程序支持类型2，类型1为仅桌面。

当软件组件 INF 文件指定**AddSoftware**时，系统会将安装设备后要安装的软件排队。  不保证何时安装软件。
如果引用的软件安装失败，则系统会在引用软件组件更新时再次尝试。

在 INF DDInstall 中使用**AddSoftware**指令[**。 *DDInstall*软件**](inf-ddinstall-software-section.md)部分。

```inf
[DDInstall.Software]
AddSoftware=SoftwareName,[flags],software-install-section
```

## <a name="entries"></a>条目

*SoftwareName*

指定要安装的软件的名称。  此名称唯一地标识软件。  处理**AddSoftware**指令时，将使用来自任何驱动程序包的**AddSoftware**指令来检查以前安装的同名软件的版本。  建议将 SoftwareName 与供应商名称一起提供，例如`ContosoControlPanel`。

*flag*

指定一个或多个（运算）标志。

**0x00000000**  
**AddSoftware**指令仅处理一次。

**0x00000001**  
对于指定具有相同唯一*SoftwareName*的**AddSoftware**的每个组件设备，将处理一次**AddSoftware**指令。

*软件-安装-部分*

引用由 INF 编写器定义的部分，其中包含用于安装软件的信息。
    
## <a name="remarks"></a>备注

在 INF 文件中，每个 INF 编写器创建的节名称必须唯一，并且必须遵循用于定义节名称的常规规则。  有关这些规则的详细信息，请参阅[INF 文件的一般语法规则](general-syntax-rules-for-inf-files.md)。

**AddSoftware**指令必须在 INF 文件中的其他位置引用已命名的*软件安装部分*。  每个此类部分都具有以下形式：

```inf
[software-install-section]

SoftwareType=type-code
[SoftwareBinary=path-to-binary]
[SoftwareArguments=argument[, argument] …]
[SoftwareVersion=w.x.y.z]
[SoftwareID=pfn://x.y.z]
```

>[!NOTE]
>有关节项和值的约束的信息，请参阅[**SoftwareType**](#software-install-section-softwaretype) 。

使用**AddSoftware**安装的任何软件必须以静默方式安装（或无提示）。 换句话说，安装过程中不会向用户显示任何用户界面。

如果卸载了虚拟软件组件设备或其父设备，则**不**会卸载使用**AddSoftware**安装的任何软件。 如果软件不是 UWP 应用（即，使用的**AddSoftware**的值为1），请确保用户可以轻松地将其卸载，而不会在注册表中留下跟踪。 为此，请执行以下操作：

* 如果使用的是 MSI 安装程序，请在应用程序的 Windows Installer 包中设置 "[添加/删除程序](https://docs.microsoft.com/windows/desktop/Msi/configuring-add-remove-programs-with-windows-installer)" 项。
* 如果使用的是安装全局注册表/文件状态的自定义 EXE （而不是补充本地设备设置），请使用[卸载注册表项](https://docs.microsoft.com/windows/desktop/Msi/uninstall-registry-key)。 

## <a name="software-install-section-softwaretype"></a>[SoftwareType]：

`SoftwareType={type-code}`

**SoftwareType**指定软件安装的类型，并且是必需的条目。

如果值为1，则表示关联的软件为 MSI 或 EXE 二进制。  如果设置了此值，则还需要**SoftwareBinary**项。  值1在 Windows 10 S 上不受支持。  

如果**SoftwareType**设置为1，则还需要**SoftwareBinary**和**SoftwareVersion** ，但**SoftwareArguments**和 flags （在**AddSoftware**指令中）是可选的。 

从 Windows 10 版本1709开始，值2指示关联软件是 Microsoft Store 链接。  仅对没有图形用户界面的特定于设备的软件使用1值。  如果有特定于设备的应用包含图形元素，则它应来自 Microsoft Store，驱动程序应使用**SoftwareType** 2 来引用它。

如果**SoftwareType**设置为2，则需要**SoftwareID** ，且 flags （在**AddSoftware**指令中）是可选的。 如果**SoftwareType**设置为2，则不使用**SoftwareBinary**和**SoftwareVersion** 。

>[!NOTE]
>使用 AddSoftware 指令类型2时，无需使用组件 INF。  指令可以在任何 INF 中成功使用。  但是，必须在组件 INF 中使用类型为1的 AddSoftware 指令。

不要使用 AddSoftware 来分发与设备无关的软件。 例如，不应使用 AddSoftware 安装特定于 OEM 的 PC 实用程序。
改为使用下列选项之一在 Windows 10 的 OEM 映像中预安装应用：

* 若要预安装 Win32 应用，请启动到审核模式并安装该应用。 有关详细信息，请参阅[审核模式概述](https://docs.microsoft.com/windows-hardware/manufacture/desktop/audit-mode-overview)。
* 若要预安装 Microsoft Store （UWP）应用，请参阅[适用于桌面设备的 Preinstallable 应用](https://docs.microsoft.com/windows-hardware/customize/preinstall/preinstallable-apps-for-windows-10-desktop)

有关将驱动程序与通用 Windows 平台（UWP）应用配对的信息，请参阅[将驱动程序与通用 Windows 平台（uwp）应用](pairing-app-and-driver-versions.md)和[硬件支持应用配对（HSA）：驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)。

## <a name="software-install-section-softwarebinary"></a>[SoftwareBinary]：

`SoftwareBinary={filename}`

指定可执行文件的路径。  系统将生成如下命令行：

`MSI: msiexec /i "<SoftwareBinary>” ALLUSERS=1 /quiet /qn /promptrestart [<SoftwareArguments>]`

`EXE: <SoftwareBinary> [<SoftwareArguments>]`

如果使用此项，则必须将可执行文件添加到 DriverStore，方法是使用**DestinationDirs**值13指定[INF CopyFiles 指令](inf-copyfiles-directive.md)。

>[!NOTE]
>有关**SoftwareBinary**项和值的约束的信息，请参阅[**SoftwareType**](#software-install-section-softwaretype) 。

## <a name="software-install-section-softwarearguments"></a>[SoftwareArguments]：

`SoftwareArguments={argument1[, argument2[, … argumentN]]}`

指定要追加到命令行的扩展插件特定参数。  可以指定系统只传递到生成的命令行的命令行参数。  还可以指定称为*运行时上下文变量*的特殊字符串。  指定运行时上下文变量时，系统会将其转换为特定于设备的值，然后再将其追加到生成的命令行。  可以使用运行时上下文变量来混合和匹配文本字符串参数。  支持的运行时上下文变量包括：

`<<DeviceInstanceID>>`

系统将上面的字符串替换为软件组件的设备实例 ID。

例如：

```inf
    [DDInstall.Software]
    AddSoftware=ContosoControlPanel,,Contoso_ControlPanel_Software

    [Contoso_ControlPanel_Software]
    SoftwareType=1
    SoftwareBinary=ContosoControlPanel.exe
    SoftwareArguments=<<DeviceInstanceID>>
    SoftwareVersion=1.0.0.0
```

上面的示例生成如下所示的命令行：

`<DriverStorePath>\ContosoControlPanel.exe PCI\VEN_0000&DEV_0001&SUBSYS_00000000&REV_00\0123`

如果 SoftwareArguments 包含多个参数：

```inf
    SoftwareArguments=arg1,<<DeviceInstanceID>>,arg2
```

以上结果为：

`<DriverStorePath>\ContosoControlPanel.exe arg1 PCI\VEN_0000&DEV_0001&SUBSYS_00000000&REV_00\0123 arg2`

>[!NOTE]
>有关**SoftwareArguments**项和值的约束的信息，请参阅[**SoftwareType**](#software-install-section-softwaretype) 。

## <a name="software-install-section-softwareversion"></a>[SoftwareVersion]：

`SoftwareVersion={w.x.y.z}`

指定软件版本。  每个值不应超过65535。  当系统遇到重复的**SoftwareName**时，它会对照前面的**SoftwareVersion**检查**SoftwareVersion** 。  如果更大，Windows 将运行该软件。

>[!NOTE]
>有关**SoftwareVersion**项和值的约束的信息，请参阅[**SoftwareType**](#software-install-section-softwaretype) 。

## <a name="software-install-section-softwareid"></a>[SoftwareID]：

`SoftwareID={x.y.z}`

指定 Microsoft Store 标识符和标识符类型。  目前仅支持包系列名称（PFN）。  使用 PFN 通过窗体`pfn://<x.y.z>`引用通用 WINDOWS 平台（UWP）应用。

>[!NOTE]
>有关**SoftwareID**项和值的约束的信息，请参阅[**SoftwareType**](#software-install-section-softwaretype) 。

## <a name="see-also"></a>另请参阅

* [使用组件 INF 文件](using-a-component-inf-file.md)。
* [INF DDInstall.Software 节](inf-ddinstall-software-section.md)
* [INF AddComponent 指令](inf-addcomponent-directive.md)
* [将驱动程序与通用 Windows 平台 (UWP) 应用配对](pairing-app-and-driver-versions.md)
* [硬件支持应用（HSA）：驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
