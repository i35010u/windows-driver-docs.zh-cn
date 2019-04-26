---
title: 创作更新驱动程序包
description: 本主题提供有关创作更新驱动程序包的信息，并提供示例 INF 文件设置和配置。
ms.assetid: 9018900A-3670-4C78-9094-1DDAB82847DD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1644d0f152627fb8f043160bbf8ee514edcf9a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328103"
---
# <a name="authoring-an-update-driver-package"></a>创作更新驱动程序包


这是必需的更新负载 ESRT 中所述的每个固件资源是捆绑在一起并使其能够维护其自己的版本控制方案，而受限于其他固件资源以便其自己的驱动程序包中分发的更新可能不是更新的频率。

下面的示例提供一个示例驱动程序的目标资源更新固件包 INF 文件定义 {SYSTEM\_固件} ESRT 示例在表 2 中，从第 1 版更新到版本 2 中的资源。 出于参考目的，我们假设为系统分配 GUID\_固件资源是 6bd4efb9-23cc-4b4a-ac37-016517413e9a。

```INF
[Version]
Signature   = "$WINDOWS NT$"
Provider    = %Provider%
Class       = Firmware
ClassGuid   = {f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
DriverVer   = 01/01/2012,2.0.0.0
CatalogFile = catalog.cat
PnpLockdown = 1

[Manufacturer]
%MfgName% = Firmware,NTarm

[Firmware.NTarm]
%FirmwareDesc% = Firmware_Install,UEFI\RES_{6bd4efb9-23cc-4b4a-ac37-016517413e9a}

[Firmware_Install.NT]
CopyFiles = Firmware_CopyFiles

[Firmware_CopyFiles]
firmware.bin

[Firmware_Install.NT.Hw]
AddReg = Firmware_AddReg

[Firmware_AddReg]
HKR,,FirmwareId,,{6bd4efb9-23cc-4b4a-ac37-016517413e9a}
HKR,,FirmwareVersion,%REG_DWORD%,0x00000002
HKR,,FirmwareFilename,,{6bd4efb9-23cc-4b4a-ac37-016517413e9a}\firmware.bin

[SourceDisksNames]
1 = %DiskName%

[SourceDisksFiles]
firmware.bin = 1

[DestinationDirs]
DefaultDestDir = %DIRID_WINDOWS%,Firmware\{6bd4efb9-23cc-4b4a-ac37-016517413e9a}

[Strings]
; localizable
Provider     = "Contoso Ltd."
MfgName      = "Fabrikam Inc."
FirmwareDesc = "Fabrikam System Firmware 2.0"
DiskName     = "Firmware Update"

; non-localizable
DIRID_WINDOWS = 10
REG_DWORD     = 0x00010001
```

更改以下各节中，若要自定义您的设置。

```INF
[Version]
DriverVer --> The date on which this driver package was authored; the Driver version of this driver package. Driver version in this driver package must be greater than the current driver version
CatalogFile --> Name of the catalog file

firmware.bin --> Change all instances of firmware.bin with the name of the firmware image name

[Manufacturer]
%MfgName% = Firmware,NTarm
[Firmware.NTarm] --> Change the architecture. 
For x86, it should be NTx86
For AMD64, it should be NTamd64

[Firmware.NTarm]
%FirmwareDesc% = Firmware_Install,UEFI\RES_{6bd4efb9-23cc-4b4a-ac37-016517413e9a} --> The GUID of the firmware resource

[Firmware_AddReg]
HKR,,FirmwareId,,{6bd4efb9-23cc-4b4a-ac37-016517413e9a} --> The GUID of the firmware resource
HKR,,FirmwareVersion,%REG_DWORD%,0x00000002 --> Version of the firmware for the update
HKR,,FirmwareFilename,,{6bd4efb9-23cc-4b4a-ac37-016517413e9a}\firmware.bin --> The subdirectory named after the GUID of the firmware resource and the firmware image name

[DestinationDirs]
DefaultDestDir = %DIRID_WINDOWS%,Firmware\{6bd4efb9-23cc-4b4a-ac37-016517413e9a} --> The full destination path for the firmware image file based under a subdirectory named after the GUID of the firmware resource within the %SystemRoot%\Firmware directory

[Strings]
; localizable
Modify any strings here [optional]
```

下表介绍的各种驱动程序程序包 INF 部分和上面的示例驱动程序包 INF 文件定义引用的字段。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>部分/字段</th>
<th>值</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>[Version]</strong></td>
<td></td>
<td>定义驱动程序的包版本控制信息。</td>
</tr>
<tr class="even">
<td>提供程序</td>
<td><p>%Provider% = Contoso Inc.</p>
<p>（在 [Strings] 部分中已本地化）</p></td>
<td>标识提供程序/整个固件资源更新驱动程序包的供应商。</td>
</tr>
<tr class="odd">
<td>Class/ClassGuid</td>
<td><p>固件 /</p>
<p>{f2e7dd72-6468-4e36-b6f1-6488f42c1b52}</p></td>
<td>指定驱动程序包的日期。 日期和版本应同时反映的日期和实际固件资源更新的版本为尽可能为了确保即插即用设备安装系统可以准确地选择最佳的驱动程序包在系统上可用。</td>
</tr>
<tr class="even">
<td>CatalogFile</td>
<td>catalog.cat</td>
<td>指定符号驱动程序程序包 INF 文件和所有关联的固件资源更新二进制文件的关联的目录文件。</td>
</tr>
<tr class="odd">
<td>PnpLockdown</td>
<td>1</td>
<td>还支持即插即用驱动程序文件锁定机制，以防止安装的驱动程序文件由不相关的应用程序外部被修改。 有关资源的固件更新，此设置应始终启用以确保不受控制的即插即用系统篡改固件资源图像文件。</td>
</tr>
<tr class="even">
<td><strong>[Manufacturer]</strong></td>
<td></td>
<td>列出所有非重复的驱动程序制造商/供应商定义的资源固件更新。 每个制造商行指定 [&lt;模型&gt;] 部分，并标识其支持的目标平台。</td>
</tr>
<tr class="odd">
<td><p>%MfgName%</p></td>
<td><p>Fabrikam Inc.</p>
<p>（在 [Strings] 部分中已本地化）</p></td>
<td>标识制造商/固件资源更新的供应商。 这可能是与提供程序字段相同。</td>
</tr>
<tr class="even">
<td></td>
<td><p>固件，</p>
<p>NTarm</p></td>
<td>标识&lt;模型&gt;] 部分，用于定义此驱动程序包，包括其目标驱动程序平台支持的固件资源设备。 在此示例中，驱动程序将仅针对基于 ARM 的 NT 平台和 [&lt;模型&gt;] 节是 [Firmware.NTarm]。</td>
</tr>
<tr class="odd">
<td><strong>[Firmware.NTarm]</strong></td>
<td></td>
<td>[&lt;模型&gt;] 列出为其定义更新的所有固件资源设备的基于 ARM 的 NT 平台的部分。 每个硬件模型线指定 [&lt;DDInstall&gt;] 部分和其相关联的硬件 ID 匹配项。</td>
</tr>
<tr class="even">
<td>%FirmwareDesc%</td>
<td><p>Fabrikam 系统固件 2.0</p>
<p>（在 [Strings] 部分中已本地化）</p></td>
<td>本文介绍固件资源更新。 这是用于设备管理器中呈现的关联的固件资源设备实例的主要说明字符串和其他设备相关的 UI。 出于此原因，说明可能包括固件供应商和版本。</td>
</tr>
<tr class="odd">
<td></td>
<td><p>Firmware_Install，</p>
<p>UEFI\RES_{RESOURCE_GUID}</p></td>
<td>标识 [&lt;DDInstall&gt;] 部分，其中包含安装固件资源更新，以标识 UEFI\RES_ {RESOURCE_GUID} 硬件 id 的设备实例为目标的步骤 其中 RESOURCE_GUID 是正在更新的固件资源的 GUID。</td>
</tr>
<tr class="even">
<td><p><strong>[Firmware_Install.NT]</strong></p>
<p>CopyFiles = Firmware_CopyFiles</p>
<p><strong>[Firmware_CopyFiles]</strong></p>
<p>...</p></td>
<td></td>
<td>[&lt;DDInstall&gt;] 节，其中包含安装固件资源更新的步骤。 有关资源的固件更新，这只定义固件资源图像文件复制到固件资源更新的位置。 在此示例中，[&lt;DDInstall&gt;] 节是 [Firmware_Install.NT]。</td>
</tr>
<tr class="odd">
<td><em>firmware.bin</em></td>
<td></td>
<td>指定要复制的固件资源更新图像文件。 请参阅下面有关复制此文件的位置的详细信息的部分 [DestinationDirs]。</td>
</tr>
<tr class="even">
<td><p><strong>[Firmware_Install.NT.Hw]</strong></p>
<p>AddReg = Firmware_AddReg</p>
<p><strong>[Firmware_AddReg]</strong></p>
<p>...</p></td>
<td></td>
<td>[&lt;DDInstall&gt;。包含固件资源更新的特定于硬件的安装步骤的 Hw] 部分。 固件资源更新，这设置在目标设备实例的设备硬件项下的注册表值的窗体中定义的固件资源更新配置信息。</td>
</tr>
<tr class="odd">
<td>FirmwareId</td>
<td>{RESOURCE_GUID}</td>
<td>固件更新的固件资源 GUID。 请注意，这是相同的固件资源嵌入在 UEFI\RES_ {RESOURCE_GUID} 硬件 ID 的 GUID，但必须指定为独立值因为即插即用系统视为严格的设备使用的不透明字符串的所有硬件 Id，此处 /驱动程序匹配目的。</td>
</tr>
<tr class="even">
<td>FirmwareVersion</td>
<td>0x00000002</td>
<td>指定为 REG_DWORD 值固件资源更新的固件版本。</td>
</tr>
<tr class="odd">
<td>FirmwareFilename</td>
<td>{RESOURCE_GUID}&lt;em&gt;firmware.bin</em></td>
<td>固件资源更新更新 Capsule 图像文件名固件文件名。 此路径是相对于 %SystemRoot%\Firmware 目录，使得 {RESOURCE_GUID} 表示用于将组织的特定固件资源所针对的所有固件图像文件的子目录。</td>
</tr>
<tr class="even">
<td><strong>[SourceDisksNames]</strong></td>
<td></td>
<td>列出了相关的驱动程序文件，例如固件更新资源图像文件，其中包含的所有非重复的驱动程序程序包源磁盘位置。</td>
</tr>
<tr class="odd">
<td>1</td>
<td><p>%Diskname%= 固件更新</p>
<p>（在 [Strings] 部分中已本地化）</p></td>
<td>指定任意带编号的驱动程序程序包源磁盘 ID 和及其说明的名称。 任何驱动程序文件关联到此磁盘 ID，如固件更新映像源文件，应直接在 INF 文件旁边 live 不指定任何可选驱动程序包相对的子目录。</td>
</tr>
<tr class="even">
<td><strong>[SourceDisksFiles]</strong></td>
<td></td>
<td>列出所引用的驱动程序包的所有驱动程序文件并链接到磁盘 ID 从 [SourceDisksNames] 部分。</td>
</tr>
<tr class="odd">
<td><em>firmware.bin</em></td>
<td>1</td>
<td>建立<em>firmware.bin</em>固件更新映像源文件为驱动程序包的一部分通过将其链接到主磁盘 id。 指定没有可选的特定于文件的子目录，因此此驱动程序文件应相对于其磁盘 live ID 子目录中，这在此情况下是正确的 INF 文件旁边。</td>
</tr>
<tr class="even">
<td><strong>[DestinationDirs]</strong></td>
<td></td>
<td>列出所引用的驱动程序包的所有驱动程序文件的目标目标目录。</td>
</tr>
<tr class="odd">
<td>DefaultDestDir</td>
<td><p>%DIRID_WINDOWS%,Firmware&lt;/p&gt;
<p>{RESOURCE_GUID}</p></td>
<td>指定复制此驱动程序包是 %systemroot%\firmware，其中 DIRID_WINDOWS (10) 表示基 %systemroot%目录，{RESOURCE_GUID} 表示子目录名称之后的所有驱动程序文件的默认目标目录固件的资源 GUID。</td>
</tr>
<tr class="even">
<td><strong>[Strings]</strong></td>
<td></td>
<td>定义键/值映射的所有间接字符串标记 （%token%)在驱动程序程序包 INF 文件中。 使用字符串令牌，可以轻松地通过引入特定于区域设置本地化的驱动程序程序包 INF 文件 [字符串。&lt;LanguageID&gt;] 部分。 它还可用于定义常数值，例如 REG_DWORD 字符串令牌替换。</td>
</tr>
<tr class="odd">
<td>提供程序</td>
<td>"Contoso Ltd."</td>
<td>字符串标记的键/值映射的示例。</td>
</tr>
</tbody>
</table>



务必使用每个固件资源更新图像文件版本的唯一名称以避免与其他固件映像的任何潜在的冲突文件，同时你自己和来自其他固件供应商。 例如， *firmware.bin*从上述应分配要满足这两个供应商名称和版本约束的以下名称：*Fabrikam 系统固件 2.0.bin*。

为了确保中相同的 Windows 系统映像部署时，可能用于 OEM/IHV 自定义目的的给定的固件资源更新映像的变体不会发生冲突，建议每个非重复固件资源更新映像是在 %systemroot%中的子目录下维护\\固件目录。 此子目录的命名应当后目标固件资源 GUID。 例如，以下固件资源更新映像路径满足部署约束: %systemroot%\\固件\\{6bd4efb9-23cc-4b4a-ac37-016517413e9a}\\Fabrikam 系统固件 2.0.bin。

## <a name="test-signing-the-firmware-driver-package"></a>测试签名固件驱动程序包


驱动程序程序包 INF 文件和固件负载二进制准备就绪后，整个驱动程序包必须以便生成编录文件进行签名。 此目录文件保证的有效性和 INF 文件和固件有效负载的二进制若要启用 Windows 安全启动固件资源更新驱动程序包中包含的真实性至关重要。

下面枚举了自签名测试目的的驱动程序包的步骤。 请注意，这些步骤是仅用于测试目的。 在生产中，固件更新驱动程序包必须提交到合作伙伴中心进行签名。 生产固件驱动程序程序包进行签名的步骤，请参阅[Certifying 和签名的更新包](certifying-and-signing-the-update-package.md)。

1.  安装最新的 Windows SDK 和 Windows 驱动程序工具包。 这将安装 makecert、 pvk2pfx inf2cat 和 signtool 工具 %systemdir%下的\\Program Files (x86)\\Windows 工具包\\&lt;*版本*&gt; \\bin\\x86。
2.  运行以下命令以创建测试证书。

    ```console
    makecert.exe -r -pe -a sha256 -eku 1.3.6.1.5.5.7.3.3 -n CN=Foo -sv fwu.pvk fwu.cer
    pvk2pfx.exe -pvk fwu.pvk -spc fwu.cer -pi <Password entered during makecert prompt> -spc fwu.cer -pfx fwu.pfx
    ```

    有关详细信息，请参阅[ **MakeCert**](https://msdn.microsoft.com/library/windows/hardware/ff548309)。

3.  运行以下命令以创建编录文件。

    ```console
    Inf2Cat.exe /driver:"." /os:8_x64
    ```

    */Driver*参数指向 INF 所在的位置。 更改的值 */os*参数取决于为其固件驱动程序包适用于 OS。 有关详细信息，请参阅[ **Inf2Cat**](https://msdn.microsoft.com/library/windows/hardware/ff547089)。

    有关安全目录和驱动程序的详细信息，请参阅[目录文件和数字签名](https://msdn.microsoft.com/library/windows/hardware/ff537872)并[为 PnP 驱动程序包创建编录文件](https://msdn.microsoft.com/library/windows/hardware/ff540161)。

4.  运行以下命令对目录文件进行签名。

    ```console
    signtool sign /fd sha256 /f fwu.pfx /p <Password entered during makecert prompt> delta.cat
    ```

    有关详细信息，请参阅[ **SignTool**](https://msdn.microsoft.com/library/windows/hardware/ff551778)。

5.  在测试系统上安装测试证书：
    1.  双击 fwu.cer 文件，然后选择**安装证书**选项。
    2.  证书安装过程中选择以下选项：
        -   对于存储位置，选择**本地计算机**。
        -   为证书存储中，浏览并选择**受信任的根证书颁发机构**。

6.  禁用安全启动固件/BIOS 选项中。
7.  启用测试签名 BCD 选项中，以便操作系统加载程序可以在启动期间加载固件图像文件 (firmware.bin)，即使该目录不是生产签名。 使用管理员权限运行以下命令：

    ```console
    bcdedit /set testsigning on
    ```

驱动程序包进行签名之后，它可以安装使用以下机制之一：

-   **设备管理器**。 对于手动测试，设备管理器提供了友好接口以查找固件资源设备并更新其驱动程序才能启动固件资源更新。
    1.  查看连接的设备的同时查看按类型，或在"Microsoft UEFI 符合系统"设备的设备时找到所需的固件资源设备下的"固件"类。
    2.  固件资源设备上右键单击并选择"更新驱动程序软件..."选项。
    3.  使用"浏览计算机以查找驱动程序软件"选项可以找到并安装到固件资源设备上的较新固件资源更新驱动程序包。 此操作将确保指定的固件资源更新驱动程序包实际上是比任何现有固件资源更新的驱动程序包的上可能已经有固件资源设备之前将其添加到 Windows 驱动程序存储区和启动安装。
-   **pnputil**。 对于自动测试，pnputil 命令行实用工具可用于从管理员提升的命令提示符固件资源更新驱动程序包导入 Windows 驱动程序存储区并启动所有适用的固件上的设备安装目前使用的是较旧固件资源版本，如由其当前安装的驱动程序程序包 INF 文件的 DriverVer 或第三缺乏资源设备完全方提供的驱动程序包 INF 文件。 例如，使用以下命令行来添加和安装 x:\\firmware.inf:

    ```console
    pnputil -i -a X:\firmware.inf
    ```

    **请注意**pnputil 工具不支持 Windows 10 移动设备上。



如果固件资源更新已成功安装固件资源设备上，并且它会提供最新的固件版本，较高的版本的固件资源更新则设备将等待系统重新启动才能完成更新操作。 处于此状态的设备将指示其需要系统重新启动的维护设备问题，这会阻止从正在启动和还原到稳定状态，直到执行重启设备。

## <a name="validating-the-status-of-the-firmware-update"></a>验证固件更新的状态


已成功安装，即插即用固件驱动程序包时将请求重新启动系统才能应用更新。 后重新启动，可以验证更新的状态。 以下注册表项下维护更新的状态：HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\控制\\FirmwareResources\\{资源\_GUID}。

资源\_GUID 是已更新 （从 ESRT) 资源的 GUID。

"LastAttemptStatus"注册表值指示固件更新，其中值为 0 表示成功，任何非零值表示失败的状态。 此注册表项的值是由操作系统加载程序基于从 ESRT LastAttemptStatus 的值填充的 NTSTATUS 代码。 下表将 LastAttemptStatus 代码映射到其相应的 NTSTATUS 代码。

| LastAttemptStatus                        | 代码 | NTSTATUS                        | 代码       |
|------------------------------------------|------|---------------------------------|------------|
| 成功                                  | 0    | 状态\_成功                 | 0x00000000 |
| 错误：不成功                      | 1    | 状态\_未成功            | 0xC0000001 |
| 错误：资源不足            | 2    | 状态\_不足\_资源 | 0xC000009A |
| 错误：版本不正确                 | 3    | 状态\_修订\_不匹配      | 0xC0000059 |
| 错误：无效的图像格式              | 4    | 状态\_无效\_映像\_格式  | 0xC000007B |
| 错误：身份验证错误              | 5    | 状态\_访问\_被拒绝          | 0xC0000022 |
| 错误：电源事件，未连接的交流     | 6    | 状态\_电源\_状态\_无效   | 0xC00002D3 |
| 错误：电源事件，没有足够的电池 | 7    | 状态\_不足\_电源     | 0xC00002DE |



固件资源设备节点的硬件 ID 属性也应反映的固件版本，其中 XXX 是新的固件版本中的更改。

-   UEFI\\RES\_{RESOURCE\_GUID}&REV\_XXX

如果固件更新失败，则可以重试失败的固件更新：

-   在设备管理器中，展开固件节点，右键单击固件资源设备，然后单击**更新驱动程序软件**。
-   单击**浏览计算机以查找驱动程序软件**，并在下一页上，单击**让我在我的计算机上从设备驱动程序的列表中选取**。
-   选择之前安装相同的驱动程序，然后单击确定。

下一步重新启动后，操作系统加载程序将调入 UpdateCapsule() 具有固件驱动程序包的有效负载。

## <a name="related-topics"></a>相关主题

[ESRT 表定义](esrt-table-definition.md)  

[Plug and play 设备](plug-and-play-device.md)  

[处理更新](processing-updates.md)  

[设备 I/O 从 UEFI 环境](device-i-o-from-the-uefi-environment.md)  

[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  

[固件更新状态](firmware-update-status.md)  
