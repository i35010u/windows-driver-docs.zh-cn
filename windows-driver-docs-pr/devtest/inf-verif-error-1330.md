---
title: InfVerif 错误 1330
description: InfVerif (InfVerif.exe) 是一种工具，可用于测试的驱动程序 INF 文件。 除了报告 INF 语法问题，该工具将报告 INF 文件是否通用。
ms.assetid: 6F565E1C-C6FC-4637-B476-FE4E4672CCC3
ms.date: 03/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: c55513476815ed35ab8931318b7491fc3a7c8b93
ms.sourcegitcommit: 56599ec634b3a731f2d13dff686be3b7b95390e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2019
ms.locfileid: "58419569"
---
# <a name="infverif-error-1330---1333"></a>InfVerif 错误 1330年 1333

InfVerif 错误 1330年有助于防止其中一个目标文件被覆盖由多个源代码文件的功能错误。 例如：

```command
[CopyFiles.A]
DesiredFileName1,SourceFile1A ; Used by DDInstallSection A

[CopyFiles.B]
DesiredFileName1,SourceFile1B ; Used by DDInstallSection B
```

当多个[DDInstall 部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)复制到单个目标文件使用不同的源文件[CopyFiles](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)指令，这些**CopyFiles**如果可能发生冲突**DDInstall 部分**全部得到处理同一系统上。 此示例是如果两个不同的设备使用相同的驱动程序但不同的安装的部分中，或在某些脱机驱动程序映像和部署方案。 因为多个源代码文件中的不同**DDInstall 部分**复制到同一确切的单个目标文件中，从不同的不同源文件**DDInstall 部分**覆盖每个其他，以便最后一个文件复制是放置目标，这可能不是预期的结果中。

## <a name="cases"></a>用例

本文档提供有关如何删除在以下情况下的功能错误的方法更新旧语法的指导。 并非所有情况下下面列出了，因为可能有其他特定于每个 INF 的原因。

* 不同**DDInstall 部分**重命名为一个服务二进制服务

* 不同**DDInstall 部分**重命名源文件以获取复制到驱动程序或用户模式应用程序访问的目标文件位置

### <a name="different-ddinstall-sections-rename-a-service-binary-for-one-service"></a>不同**DDInstall 部分**重命名为一个服务二进制服务

下面的代码是举例说明如何将不同**DDInstall 部分**可能重命名为一个服务二进制服务：

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

若要更新此代码，创建不同的二进制文件的不同的服务名称：

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

### <a name="different-ddinstall-sections-rename-a-source-file-to-get-copied-over-to-a-destination-file-location-accessed-by-the-driver-or-a-user-mode-application"></a>不同**DDInstall 部分**重命名源文件以获取复制到驱动程序或用户模式应用程序访问的目标文件位置

在这种情况下，该驱动程序正在访问正用作动态文件位置的固定的文件位置。 若要有一个动态的变量，跟踪多个源文件，可以使用[AddReg](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive) HKR 条目来存储可在运行时检索到的路径。 这样做的原因**AddReg** HKR 项存储相对于设备。

**AddReg** HKR 条目指定源代码文件，而不是选择要复制到源文件的单个目标文件的文件位置：

```command
[A.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1A"

[B.AddReg]
HKR,, FileName1Path, "%13%\SourceFile1B"
```

而不是固定的文件位置的访问，可以从设备上设置检索目标文件的位置。 目标文件位置是存储在注册表值中的 INF，检索通过驱动程序中的 API 调用。

若要预配通过 INF 值，请使用[INF AddReg 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)使用 HKR *reg 根*中的条目*添加注册表部分*引用从[INF DDInstall 部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)或[INF DDInstall.HW 部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)。

因为目标文件而不是单个目标文件位置跟踪的注册表值，该驱动程序将需要以不同的方式访问这些文件。 若要访问的目标文件，该驱动程序现在必须调用到一个打开的注册表值并将其返回该源文件的位置的以下 Api:

#### <a name="wdm"></a>WDM

* [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)

#### <a name="wdf"></a>WDF

* [**WdfDeviceOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)

* [**WdfFdoInitOpenRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey)

#### <a name="other-user-mode-code"></a>其他用户模式代码

* [**CM_Open_DevNode_Key**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key)

> [!NOTE]
> 在此示例中，文件 INF 有效负载的目标位置不影响该解决方案。  但是，若要使用的最佳做法，该示例使用[DIRID](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids) 13，因为它提供更快的安装通过更少的文件副本。  请参阅"[使用 DIRIDs](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids)"和"[从驱动程序存储区中运行](https://docs.microsoft.com/windows-hardware/drivers/develop/universal-driver-scenarios#run-from-the-driver-store)"有关详细信息。

下面的代码示例演示如何更新使用旧语法 INF。

### <a name="details-for-different-source-files-mapped-to-one-destination-file"></a>映射到一个目标文件不同的源文件的详细信息

<table>
<thead>
<tr>
<th>源代码</th>
<th>备注</th>
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
<td></br>选择文件转手动</td>
</tr>
<tr>
<td><pre>[CopyFiles.A]
DesiredFileName1,SourceFile1A ; HW Version A
DesiredFileName2,SourceFile2A ; HW Version A</br>
[CopyFiles.B]
DesiredFileName1,SourceFile1B ; HW Version B
DesiredFileName2,SourceFile2B ; HW Version B
</pre></td>
<td></br><u>文件复制技术</u>:重命名文件，以便安装 DDInstall 部分会选取要获取复制到驱动程序链接到的目标文件路径的源文件。

这不起作用的用例，在安装之前将所有 DDInstall 部分的所有文件被都复制。
</td>
</tr>
</tbody>
</table>

### <a name="details-for-udating-by-using-addreg-hkr-entries"></a>通过使用 AddReg HKR 条目 udating 的详细信息

<table>
<thead>
<tr>
<th>源代码</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr>
<td><pre>[DestinationDirs]
CopyFiles.A = 13
CopyFiles.B = 13
</td>
</pre>
<td></br>最佳做法是将驱动程序中的所有项存储区目录 (Dirid 13)</td>
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

<td></br>添加 AddReg 部分为每个 DDInstall Section.HW 来跟踪该安装所需的文件。

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
<td></br>多个源文件位置映射到一个注册表值。 这样做的原因 HKR AddReg DDInstall 或 DDInstall.HW 部分从存储在设备设置。  使用此驱动程序包安装设备时，它将仅使用 DDInstall 部分之一以便将使用只有一个 HKR AddReg 并不会冲突。
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
<td></br>因此没有功能错误和 INF 传递 InfVerif，所有文件将映射到它们自身位置。
</br>
不要使用 CopyFiles 重命名为其 DestinationDirs 包括 Dirid 13 文件。

</td>
</tr>
</tbody>
</table>

### <a name="accessing-the-file-location-from-the-driver-pseudo-code"></a>从驱动程序 （伪代码） 访问的文件位置

```command
Before (Fixed Filename):
    OpenFile(Path\DesiredFileName1)

After (Dynamic Filename):
    OpenDeviceRegistryKey(Device, &KeyHandle)
    RegistryKeyQueryValue(KeyHandle, FileNamePath1, &SourceFile)
    OpenFile(SourceFile)
```

### <a name="accessing-the-file-location-from-user-mode"></a>从用户模式下访问的文件位置

当从用户模式下访问目标文件，不会具有驱动程序包含的设备上下文。 在这种情况下，您需要添加一个额外的步骤。 打开密钥句柄之前, 查找包含注册表值，该值指示要加载的文件的设备。

这[链接](https://docs.microsoft.com/en-us/windows-hardware/drivers/develop/universal-driver-scenarios#run-from-the-driver-store)演示如何筛选设备列表，以便查找你的设备和用户模式下，使用的最佳做法 Dirid 13 中打开的句柄注册表位置。

## <a name="errors-1331---1333"></a>错误 1331年 1333

错误 1331年 1333年是所有相同的问题，但与注册表值，注册表值在服务中，并分别服务。 有关解决错误 1331年 1333年的错误 1330年封面方法的文档中的示例。
