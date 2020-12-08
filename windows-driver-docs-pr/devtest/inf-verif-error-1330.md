---
title: InfVerif 错误 1330
description: 'InfVerif ( # A0) 是可用于测试驱动程序 INF 文件的工具。 除了报告 INF 语法问题外，该工具还报告 INF 文件是否是通用的。'
ms.date: 03/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0b2370ca820e6856697d2323f604462c3a5971c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833137"
---
# <a name="infverif-error-1330---1333"></a>InfVerif 错误 1330-1333

InfVerif 错误1330有助于避免在多个源文件覆盖一个目标文件时出现功能错误。 例如：

```command
[CopyFiles.A]
DesiredFileName1,SourceFile1A ; Used by DDInstallSection A

[CopyFiles.B]
DesiredFileName1,SourceFile1B ; Used by DDInstallSection B
```

当多个 [DDInstall 部分](../install/inf-ddinstall-section.md)使用 [CopyFiles](../install/inf-copyfiles-directive.md)指令将不同的源文件复制到单个目标文件时，如果 **DDInstall 部分** 都在同一系统上得到处理，则这些 **CopyFiles** 可能会冲突。 例如，如果两个不同的设备使用的是相同的驱动程序，但安装部分不同，或者在某些脱机驱动程序映像和部署方案中使用。 由于不同 **DDInstall 部分** 的多个源文件将复制到同一个单个目标文件，不同 **DDInstall 部分** 中的不同源文件将彼此覆盖，以使最后一个文件复制到目标中，这可能不是预期的结果。

## <a name="cases"></a>案例

本文档提供有关如何将旧语法更新为在以下情况下删除功能错误的方法的指导。 下面并未列出所有事例，因为每个 INF 都有其他特定的原因。

* 不同的 **DDInstall 节** 为一个服务重命名服务二进制文件

* 不同的 **DDInstall 节** 重命名源文件，以便将其复制到由驱动程序或用户模式应用程序访问的目标文件位置

### <a name="different-ddinstall-sections-rename-a-service-binary-for-one-service"></a>不同的 **DDInstall 节** 为一个服务重命名服务二进制文件

下面的代码示例演示了不同的 **DDInstall 节** 如何为一个服务重命名服务二进制文件：

```command
[DDInstallSection_A]
CopyFiles = CopyFiles.A

[DDInstallSection_B]
CopyFiles = CopyFiles.B

[CopyFiles.A]
ServiceBinaryFile, ServiceBinaryA

[CopyFiles.B]
ServiceBinaryFile, ServiceBinaryB

[DDInstallSection_A.Services]
AddService = ServiceName, 0x00000002, ServiceName_Install

[DDInstallSection_B.Services]
AddService = ServiceName, 0x00000002, ServiceName_Install

[ServiceName_Install]
ServiceType    = 1
StartType      = 3
ErrorControl   = 0
ServiceBinary  = %12%\ServiceBinaryFile
```

若要更新此代码，请为不同的二进制文件创建不同的服务名称：

```command
[DDInstallSection_A]
CopyFiles = CopyFiles.A

[DDInstallSection_B]
CopyFiles = CopyFiles.B

[CopyFiles.A]
ServiceBinaryA

[CopyFiles.B]
ServiceBinaryB

[DDInstallSection_A.Services]
AddService = ServiceName1, 0x00000002, ServiceName1_Install

[DDInstallSection_B.Services]
AddService = ServiceName2, 0x00000002, ServiceName2_Install

[ServiceName1_Install]
ServiceType    = 1
StartType      = 3
ErrorControl   = 0
ServiceBinary  = %12%\ServiceBinaryA

[ServiceName2_Install]
ServiceType    = 1
StartType      = 3
ErrorControl   = 0
ServiceBinary  = %12%\ServiceBinaryB
```

### <a name="different-ddinstall-sections-rename-a-source-file-to-get-copied-over-to-a-destination-file-location-accessed-by-the-driver-or-a-user-mode-application"></a>不同的 **DDInstall 节** 重命名源文件，以便将其复制到由驱动程序或用户模式应用程序访问的目标文件位置

在这种情况下，驱动程序将访问用作动态文件位置的固定文件位置。 若要让一个动态变量跟踪多个源文件，可以使用 [AddReg](../install/inf-addreg-directive.md) HKR 项来存储可在运行时检索的路径。 这是因为 **AddReg** HKR 条目是相对于设备存储的。

**AddReg** HKR 条目指定源文件的文件位置，而不是选择要将源文件复制到的单个目标文件：

```command
[A.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1A"

[B.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1B"
```

可以从设备上的设置中检索目标文件的位置，而不是访问固定文件位置。 目标文件位置由 INF 存储在注册表值中，并通过驱动程序中的 API 调用来检索。

若要通过 INF 预配这些值，请在 [Inf DDInstall 部分](../install/inf-ddinstall-section.md)或 *reg-root* [inf DDInstall 部分](../install/inf-ddinstall-hw-section.md)引用的 *添加注册表部分* 中使用 [inf AddReg 指令](../install/inf-addreg-directive.md)。

由于注册表值跟踪目标文件而不是单个目标文件位置，因此驱动程序必须以不同的方式访问这些文件。 若要访问目标文件，驱动程序现在需要调用以下 Api 之一来打开注册表值并使其返回源文件的位置：

#### <a name="wdm"></a>WDM

* [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)

#### <a name="wdf"></a>WDF

* [**WdfDeviceOpenRegistryKey**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)

* [**WdfFdoInitOpenRegistryKey**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)

#### <a name="other-user-mode-code"></a>其他用户模式代码

* [**CM_Open_DevNode_Key**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key)

> [!NOTE]
> 在此示例中，INF 负载不会影响解决方案的文件的目标位置。  但是，若要使用最佳做法，示例使用了 [DIRID](../install/using-dirids.md) 13，因为它通过更少的文件副本提供更快的安装。  有关详细信息，请参阅 "[使用 DIRIDs](../install/using-dirids.md)" 和 "[从驱动程序存储区运行](../develop/dch-example.md#run-from-the-driver-store)"。

下面的示例代码演示如何更新使用旧语法的 INF。

### <a name="details-for-different-source-files-mapped-to-one-destination-file"></a>映射到一个目标文件的不同源文件的详细信息

<table>
<thead>
<tr>
<th>源代码</th>
<th>评论</th>
</tr>
</thead>
<tbody>
<tr><td><pre>[DestinationDirs]
CopyFiles.A = 12
CopyFiles.B = 12</br>
[DDInstallSection_A]
CopyFiles  = CopyFiles.A</br>
[DDInstallSection_B]
CopyFiles = CopyFiles.B
</td>
</pre>
<td></br>选取文件的手动位置</td>
</tr>
<tr>
<td><pre>[CopyFiles.A]
DesiredFileName1,SourceFile1A ; HW Version A
DesiredFileName2,SourceFile2A ; HW Version A</br>
[CopyFiles.B]
DesiredFileName1,SourceFile1B ; HW Version B
DesiredFileName2,SourceFile2B ; HW Version B
</pre></td>
<td></br><u>文件复制技术</u>：重命名文件，使正在安装的 DDInstall 部分选择要复制到驱动程序链接到的目标文件路径的源文件。

如果所有 DDInstall 部分的所有文件都在安装之前复制，则此操作不起作用。
</td>
</tr>
</tbody>
</table>

### <a name="details-for-udating-by-using-addreg-hkr-entries"></a>使用 AddReg HKR 项的 udating 的详细信息

<table>
<thead>
<tr>
<th>源代码</th>
<th>评论</th>
</tr>
</thead>
<tbody>
<tr>
<td><pre>[DestinationDirs]
CopyFiles.A = 13
CopyFiles.B = 13
</td>
</pre>
<td></br>最佳做法是将驱动程序存储目录中的所有内容保留 (Dirid 13) </td>
</tr>
<tr>
<td><pre>[DDInstallSection_A]
CopyFiles = CopyFiles.A</br>
[DDInstallSection_A.HW]
AddReg = A.AddReg</br>
[DDInstallSection_B]
CopyFiles = CopyFiles.B</br>
[DDInstallSection_B.HW]
AddReg = B.AddReg  

</pre></td>

<td></br>为每个 DDInstall 节添加 AddReg 部分。 HW 以跟踪安装所需的文件。

</td>
</tr>

<tr>
<td><pre>[A.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1A"
HKR,, FileName2Path, "%13%\SourceFile2A"</br>
[B.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1A"
HKR,, FileName2Path, "%13%\SourceFile2A"

</pre></td>
<td></br>映射到一个注册表值的多个源文件位置。 这是因为 DDInstall 或 DDInstall 部分中的 HKR AddReg 存储在 "设备设置" 中。  当使用此驱动程序包安装设备时，它将仅使用其中一个 DDInstall 部分，因此仅使用其中一个 HKR AddReg，而不会发生冲突。
</td>
</tr>

<tr>
<td><pre>[CopyFiles.A]
SourceFile1A ; HW Version A
SourceFile2A ; HW Version A</br>
[CopyFiles.B]
SourceFile1B ; HW Version B
SourceFile2B ; HW Version B
</pre></td>
<td></br>所有文件都映射到其自己的位置，因此不会通过 InfVerif 的功能错误和 INF。
</br>
不要使用 CopyFiles 重命名 DestinationDirs 包括 Dirid 13 的文件。

</td>
</tr>
</tbody>
</table>

### <a name="accessing-the-file-location-from-the-driver-pseudo-code"></a> (伪代码从驱动程序访问文件位置) 

```command
Before (Fixed Filename):
    OpenFile(Path\DesiredFileName1)

After (Dynamic Filename):
    OpenDeviceRegistryKey(Device, &KeyHandle)
    RegistryKeyQueryValue(KeyHandle, FileNamePath1, &SourceFile)
    OpenFile(SourceFile)
```

### <a name="accessing-the-file-location-from-user-mode"></a>从用户模式访问文件位置

从用户模式访问目标文件时，不会有驱动程序具有的设备上下文。 在这种情况下，需要添加其他步骤。 打开密钥句柄之前，请查找包含用于指示要加载的文件的注册表值的设备。

请参阅 [从驱动程序存储区运行](../develop/dch-example.md#run-from-the-driver-store) ，了解如何筛选设备列表以查找设备，并在用户模式下使用 Dirid 13 获取注册表位置的句柄。

## <a name="errors-1331---1333"></a>错误 1331-1333

错误 1331-1333 是相同的问题，但与注册表值、服务中的注册表值和服务分别相关。 用于错误1330的文档中的示例涵盖了解决错误 1331-1333 的技术。
