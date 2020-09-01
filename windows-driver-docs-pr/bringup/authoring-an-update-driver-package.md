---
title: 创作更新驱动程序包
description: 本主题提供有关创作更新驱动程序包，并提供示例 INF 文件设置和配置的信息。
ms.assetid: 9018900A-3670-4C78-9094-1DDAB82847DD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12f57e949fb15d315a7329a0af3f5c61a3374da3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188911"
---
# <a name="authoring-an-update-driver-package"></a>创作更新驱动程序包


需要将 ESRT 中描述的每个固件资源的更新有效负载捆绑到其自己的驱动程序包中并将其分发到，使其能够维护其自己的版本控制方案，而不会绑定到可能不会在同一节奏上更新的其他固件资源更新。

下面的示例为固件资源更新提供了一个示例驱动程序包 INF 文件定义，该文件 \_ 从表2的 ESRT 示例中以 {SYSTEM 固件} 资源为目标，并将其从版本1更新为版本2。 出于参考目的，假设为系统固件资源分配的 GUID \_ 是6bd4efb9-23cc-4b4a-ac37-016517413e9a。

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

更改以下部分，为你的设置进行自定义。

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

下表描述了各种驱动程序包 INF 部分和字段，它们引用了上述示例驱动程序包 INF 文件定义。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>节/字段</th>
<th>值</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>版本</strong></td>
<td></td>
<td>定义驱动程序包版本信息。</td>
</tr>
<tr class="even">
<td>提供程序</td>
<td><p>% Provider% = Contoso Inc。</p>
<p> (在 [字符串] 部分中本地化) </p></td>
<td>标识整个固件资源更新驱动程序包的提供程序/供应商。</td>
</tr>
<tr class="odd">
<td>Class/ClassGuid</td>
<td><p>固件</p>
<p>{f2e7dd72-6468-4e36-b6f1-6488f42c1b52}</p></td>
<td>指定驱动程序包的日期。 日期和版本应尽可能地反映实际固件资源更新的日期和版本，以确保 PnP 设备安装系统可以准确选择系统上可用的最佳驱动程序包。</td>
</tr>
<tr class="even">
<td>CatalogFile</td>
<td>catalog.cat</td>
<td>指定关联的目录文件，该文件对驱动程序包 INF 文件和所有关联的固件资源更新二进制文件进行签名。</td>
</tr>
<tr class="odd">
<td>PnpLockdown</td>
<td>1</td>
<td>启用 PnP 驱动程序文件锁定机制，以防止不相关的应用程序在外部修改安装的驱动程序文件。 对于固件资源更新，应始终启用此设置，以确保无法在 PnP 系统控制外部篡改固件资源映像文件。</td>
</tr>
<tr class="even">
<td><strong>提供</strong></td>
<td></td>
<td>列出定义固件资源更新的所有独特的驱动程序制造商/供应商。 每个制造商行指定一个 [ &lt; 模型 &gt; ] 部分，并标识其支持的目标平台。</td>
</tr>
<tr class="odd">
<td><p>%MfgName%</p></td>
<td><p>Fabrikam Inc。</p>
<p> (在 [字符串] 部分中本地化) </p></td>
<td>标识固件资源更新的制造商/供应商。 这可以与提供程序字段相同。</td>
</tr>
<tr class="even">
<td></td>
<td><p>固件</p>
<p>NTarm</p></td>
<td>标识 " &lt; 模型" &gt; 部分，该部分定义此驱动程序包支持的固件资源设备，包括其目标驱动程序平台。 在此示例中，驱动程序只针对基于 ARM 的 NT 平台，而 [ &lt; 模型 &gt; ] 部分为 [NTarm]。</td>
</tr>
<tr class="odd">
<td><strong>[NTarm]</strong></td>
<td></td>
<td>[ &lt; 模型 &gt; ] 部分，它列出了用于定义更新的所有固件资源设备。 每个硬件型号行均指定了 [ &lt; DDInstall &gt; ] 部分及其关联的硬件 ID 匹配项。</td>
</tr>
<tr class="even">
<td>%FirmwareDesc%</td>
<td><p>Fabrikam 系统固件2。0</p>
<p> (在 [字符串] 部分中本地化) </p></td>
<td>描述固件资源更新。 这是用于在设备管理器和其他与设备相关的 UI 中显示关联的固件资源设备实例的主要描述字符串。 出于此原因，说明可能包含固件供应商和版本。</td>
</tr>
<tr class="odd">
<td></td>
<td><p>Firmware_Install，</p>
<p>UEFI \ RES_ {RESOURCE_GUID}</p></td>
<td>标识 [ &lt; DDInstall &gt; ] 节，其中包含针对 UEFI \ RES_ {RESOURCE_GUID} 硬件 ID 标识的设备实例的固件资源更新的安装步骤。 其中 RESOURCE_GUID 是要更新的固件资源的 GUID。</td>
</tr>
<tr class="even">
<td><p><strong>[Firmware_Install NT]</strong></p>
<p>CopyFiles = Firmware_CopyFiles</p>
<p><strong>[Firmware_CopyFiles]</strong></p>
<p>...</p></td>
<td></td>
<td>[ &lt; DDInstall &gt; ] 包含固件资源更新安装步骤的部分。 对于固件资源更新，这仅定义要为固件资源更新复制的固件资源映像文件。 在此示例中，[ &lt; DDInstall &gt; ] 部分为 [Firmware_Install NT]。</td>
</tr>
<tr class="odd">
<td><em>固件 bin</em></td>
<td></td>
<td>指定要复制的固件资源更新映像文件。 有关将此文件复制到的位置的详细信息，请参阅下面的 [DestinationDirs] 部分。</td>
</tr>
<tr class="even">
<td><p><strong>[Firmware_Install]</strong></p>
<p>AddReg = Firmware_AddReg</p>
<p><strong>[Firmware_AddReg]</strong></p>
<p>...</p></td>
<td></td>
<td>[ &lt; DDInstall &gt;Hw] 部分，其中包含固件资源更新的特定于硬件的安装步骤。 对于固件资源更新，此项以在目标设备实例的设备硬件密钥下设置的注册表值形式定义固件资源更新配置信息。</td>
</tr>
<tr class="odd">
<td>FirmwareId</td>
<td>{RESOURCE_GUID}</td>
<td>固件资源更新的固件 GUID。 请注意，这是嵌入在 UEFI \ RES_ {RESOURCE_GUID} 硬件 ID 中的同一固件资源 GUID，但必须将其指定为独立的值，因为 PnP 系统将所有硬件 Id 视为不透明的字符串，这些字符串严格用于设备/驱动程序匹配。</td>
</tr>
<tr class="even">
<td>FirmwareVersion</td>
<td>0x00000002</td>
<td>固件资源更新的固件版本，指定为 REG_DWORD 值。</td>
</tr>
<tr class="odd">
<td>FirmwareFilename</td>
<td>{RESOURCE_GUID} &lt;em &gt; 固件 bin</em></td>
<td>固件资源更新的更新胶囊图像文件名的固件文件名。 此路径是相对于%SystemRoot%\Firmware 目录的路径，因此 {RESOURCE_GUID} 表示一个子目录，用于组织针对特定固件资源的所有固件映像文件。</td>
</tr>
<tr class="even">
<td><strong>[SourceDisksNames]</strong></td>
<td></td>
<td>列出所有不同的驱动程序包源磁盘位置，其中包含关联的驱动程序文件，如固件更新资源映像文件。</td>
</tr>
<tr class="odd">
<td>1</td>
<td><p>% DiskName% = 固件更新</p>
<p> (在 [字符串] 部分中本地化) </p></td>
<td>指定任意编号的驱动程序包源磁盘 ID 及其说明名称。 未指定可选的驱动程序包相对子目录，因此，与此磁盘 ID 关联的任何驱动程序文件（如固件资源更新映像文件）都应直接位于 INF 文件的旁边。</td>
</tr>
<tr class="even">
<td><strong>[SourceDisksFiles]</strong></td>
<td></td>
<td>列出驱动程序包引用的所有驱动程序文件，并将其链接到 [SourceDisksNames] 部分中的磁盘 ID。</td>
</tr>
<tr class="odd">
<td><em>固件 bin</em></td>
<td>1</td>
<td>将 <em>固件 bin</em> 固件资源更新映像文件与主磁盘 ID 链接在一起，从而将其视为驱动程序包的一部分。 未指定特定的文件特定子目录，因此此驱动程序文件应相对于其磁盘 ID 的子目录实时运行，在本例中，该文件位于 INF 文件的右边。</td>
</tr>
<tr class="even">
<td><strong>[DestinationDirs]</strong></td>
<td></td>
<td>列出驱动程序包引用的所有驱动程序文件的目标目标目录。</td>
</tr>
<tr class="odd">
<td>DefaultDestDir</td>
<td><p>% DIRID_WINDOWS%，固件 &lt; /p&gt;
<p>{RESOURCE_GUID}</p></td>
<td>指定从此驱动程序包复制到%SystemRoot%\Firmware 的所有驱动程序文件的默认目标目录，其中 DIRID_WINDOWS (10) 表示基% SystemRoot% 目录，{RESOURCE_GUID} 表示固件资源 GUID 后的子目录名称。</td>
</tr>
<tr class="even">
<td><strong>Strings</strong></td>
<td></td>
<td>为驱动程序包 INF 文件中 (% token% ) 的所有间接字符串标记定义键/值映射。 使用字符串标记，通过引入特定于区域设置的 [字符串，可以轻松地本地化驱动程序包 INF 文件。 &lt;LanguageID &gt; ] 部分。 使用字符串标记替换定义常量数值（如 REG_DWORD）也很有用。</td>
</tr>
<tr class="odd">
<td>提供程序</td>
<td>Contoso 有限公司。</td>
<td>字符串标记键/值映射的示例。</td>
</tr>
</tbody>
</table>



务必为每个固件资源更新映像文件版本使用唯一的名称，以避免与其他固件映像文件（您自己）和其他固件供应商的任何潜在冲突。 例如，应为上面的 " *固件* " 分配以下名称以满足供应商名称和版本约束： *fabrikam-system-firmware-2.0*。

为了确保给定固件资源更新映像的变体（可能用于 OEM/IHV 自定义目的）在部署到同一 Windows 系统映像时不会发生冲突，建议将每个不同的固件资源更新映像维持在% SystemRoot% 固件目录中的子目录下 \\ 。 应在目标固件资源 GUID 之后指定此子目录。 例如，以下固件资源更新映像路径满足部署约束：% SystemRoot% \\ 固件 \\ {6Bd4efb9-23cc-4b4a-ac37-016517413e9a} \\ fabrikam-system-firmware-2.0。

## <a name="test-signing-the-firmware-driver-package"></a>对固件驱动程序包进行测试签名


驱动程序包 INF 文件和固件有效负载二进制文件准备就绪后，必须对整个驱动程序包进行签名，才能生成编录文件。 为了使 Windows 能够安全地启动固件资源更新，此目录文件保证在驱动程序包中包含的 INF 文件和固件有效负载二进制文件的有效性和真实性，这一点非常重要。

下面列举了用于自行签署用于测试目的的驱动程序包的步骤。 请注意，这些步骤仅用于测试目的。 在生产环境中，固件更新驱动程序包必须提交到合作伙伴中心进行签名。 有关为生产签署固件驱动程序包的步骤，请参阅对 [更新包进行验证和签名](certifying-and-signing-the-update-package.md)。

1.  安装最新的 Windows SDK 和 Windows 驱动程序工具包。 这会将 makecert、pvk2pfx inf2cat 和 signtool 工具安装 \\ (x86) \\ Windows 包 \\ &lt; *版本* &gt; \\ bin \\ x86 下的% systemdir% Program Files 下。
2.  运行以下命令来创建测试证书。

    ```console
    makecert.exe -r -pe -a sha256 -eku 1.3.6.1.5.5.7.3.3 -n CN=Foo -sv fwu.pvk fwu.cer
    pvk2pfx.exe -pvk fwu.pvk -spc fwu.cer -pi <Password entered during makecert prompt> -spc fwu.cer -pfx fwu.pfx
    ```

    有关详细信息，请参阅 [**MakeCert**](../devtest/makecert.md)。

3.  运行以下命令以创建编录文件。

    ```console
    Inf2Cat.exe /driver:"." /os:8_x64
    ```

    */Driver*参数指向 INF 所在的位置。 根据固件驱动程序包的目标 OS 更改 */os* 参数的值。 有关详细信息，请参阅 [**Inf2Cat**](../devtest/inf2cat.md)。

    有关安全目录和驱动程序的详细信息，请参阅 [目录文件和数字签名](../install/catalog-files.md) 和 [为 PnP 驱动程序包创建编录文件](../install/creating-a-catalog-file-for-a-pnp-driver-package.md)。

4.  运行以下命令对编录文件进行签名。

    ```console
    signtool sign /fd sha256 /f fwu.pfx /p <Password entered during makecert prompt> delta.cat
    ```

    有关详细信息，请参阅 [**SignTool**](../devtest/signtool.md)。

5.  在测试系统上安装测试证书：
    1.  双击 "fwu" 文件并选择 " **安装证书** " 选项。
    2.  在安装证书的过程中，请选择以下选项：
        -   对于 "存储位置"，选择 " **本地计算机**"。
        -   对于 "证书存储"，浏览并选择 " **受信任的根证书颁发机构**"。

6.  在固件/BIOS 选项中禁用安全启动。
7.  在 BCD 选项中启用测试签名，使 OS 加载程序可以在启动过程中 (固件) 加载固件映像文件，即使未对目录进行生产签名也是如此。 在管理员权限下运行以下命令：

    ```console
    bcdedit /set testsigning on
    ```

驱动程序包签名后，可以使用以下机制之一进行安装：

-   **设备管理器**。 对于手动测试，设备管理器提供了一个用于查找固件资源设备并更新其驱动程序以启动固件资源更新的友好界面。
    1.  按类型查看设备时，在 "固件" 类中找到所需的固件资源设备，或在按连接查看设备时在 "Microsoft UEFI 兼容的系统" 设备下找到所需的固件资源设备。
    2.  右键单击固件资源设备，并选择 "更新驱动程序软件 ..."选.
    3.  使用 "浏览计算机以查找驱动程序软件" 选项，查找固件资源设备并将其安装到固件资源设备上。 在将指定的固件资源更新驱动程序包添加到 Windows 驱动程序存储区并启动安装之前，此操作将确保指定的固件资源更新驱动程序包比已在固件资源设备上的任何现有固件资源更新驱动程序包更新。
-   **pnputil**。 对于自动测试，可以从管理员提升的命令提示符处使用 pnputil 命令行实用工具将固件资源更新驱动程序包导入 Windows 驱动程序存储区，并在当前使用较旧的固件资源版本的任何/所有适用的固件资源设备上启动设备安装。如 DriverVer 当前安装的驱动程序包 INF 文件或缺少第三方提供的驱动程序包 INF 文件的完全一样。 例如，使用以下命令行来添加和安装 X： \\ 固件：

    ```console
    pnputil -i -a X:\firmware.inf
    ```

    **注意**  Windows 10 移动版不支持 pnputil 工具。



如果固件资源更新已成功安装在固件资源设备上，并且它提供的固件资源更新版本高于当前固件版本，则设备将等待系统重启以完成更新操作。 处于此状态的设备将指示它需要通过维护设备问题来重新启动系统，这会阻止设备启动并还原到稳定状态，直到执行重新启动。

## <a name="validating-the-status-of-the-firmware-update"></a>验证固件更新的状态


成功安装固件驱动程序包后，PnP 将请求系统重新启动以应用更新。 重新启动后，可以验证更新的状态。 更新状态将保留在以下注册表项下： HKEY \_ LOCAL \_ MACHINE \\ SYSTEM \\ CurrentControlSet \\ Control \\ FirmwareResources \\ {RESOURCE \_ GUID}。

资源 \_ guid 是已更新的 ESRT) 中资源 (的 guid。

"LastAttemptStatus" 注册表值指示固件更新的状态，其中值为0表示成功，而任何非零值表示失败。 此注册表项的值是 OS 加载器根据 ESRT 中 LastAttemptStatus 的值填充的 NTSTATUS 代码。 下表将 LastAttemptStatus 代码映射到其对应的 NTSTATUS 代码。

| LastAttemptStatus                        | 代码 | NTSTATUS                        | 代码       |
|------------------------------------------|------|---------------------------------|------------|
| Success                                  | 0    | 状态 \_ 成功                 | 0x00000000 |
| 错误：失败                      | 1    | 状态 \_ 失败            | 0xC0000001 |
| 错误：资源不足            | 2    | 状态 \_ \_ 资源不足 | 0xC000009A |
| 错误：版本不正确                 | 3    | 状态 \_ 修订 \_ 不匹配      | 0xC0000059 |
| 错误：图像格式无效              | 4    | 状态 \_ \_ 图像 \_ 格式无效  | 0xC000007B |
| 错误：身份验证错误              | 5    | \_拒绝访问 \_ 状态          | 0xC0000022 |
| 错误：电源事件，未连接 AC     | 6    | 状态 \_ 电源 \_ 状态 \_ 无效   | 0xC00002D3 |
| 错误：电源事件，电池电量不足 | 7    | 状态 \_ \_ 电量不足     | 0xC00002DE |



固件资源设备节点的 "硬件 ID" 属性还应该反映固件版本中的更改，其中 XXX 是新固件版本。

-   UEFI \\ RES \_ {RESOURCE \_ GUID} &REV \_ XXX

如果固件更新失败，你可以重试失败的固件更新：

-   在设备管理器中，展开 "固件" 节点，右键单击固件资源设备，然后单击 " **更新驱动程序软件**"。
-   单击 " **浏览计算机以查找驱动程序软件**"，然后在下一页上单击 " **让我从计算机上的设备驱动程序列表中选择**"。
-   选择之前安装的同一驱动程序，然后单击 "确定"。

下一次重新启动后，操作系统加载程序将调用 UpdateCapsule ( # A1，其中包含固件驱动程序包的负载。

## <a name="related-topics"></a>相关主题

[ESRT 表定义](esrt-table-definition.md)  

[即插即用设备](plug-and-play-device.md)  

[处理更新](processing-updates.md)  

[来自 UEFI 环境的设备 I/O](device-i-o-from-the-uefi-environment.md)  

[无缝危机预防和恢复](seamless-crisis-prevention-and-recovery.md)  

[固件更新状态](firmware-update-status.md)