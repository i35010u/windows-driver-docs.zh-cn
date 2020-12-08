---
title: Windows 收件箱智能卡微型驱动程序
description: Windows 收件箱智能卡微型驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fad5d26b2dee8752cad51b3ddd25d479d6646c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811859"
---
# <a name="windows-inbox-smart-card-minidriver"></a>Windows 收件箱智能卡微型驱动程序

从带 Service Pack 1 (SP1) 的 Windows 7 开始，提供了一个收件箱泛型类微型驱动程序，它支持 PIV 兼容的智能卡和实现 GID 卡边缘的智能卡。

符合 PIV 标准的智能卡和卡，用于实现 GID 卡边缘。 有关 PIV 的详细信息，请参阅 [联邦员工和合同工的个人身份验证 (PIV) ](https://www.nist.gov/publications/personal-identity-verification-piv-federal-employees-and-contractors)。

有关 GID 的详细信息，请参阅 " [通用标识设备规范](/previous-versions/windows/hardware/design/dn642100(v=vs.85)) " 网页。

将智能卡插入读卡器并且基本 CSP/KSP 调用 [**CardAcquireContext**](/previous-versions/dn468701(v=vs.85))时，类微型驱动程序会执行以下发现过程，以将关联的卡标记为 PIV 或 gid 兼容：

1. 发出 SELECT 命令以查找 PIV 辅助工具。 如果此命令成功，则 Windows 将该卡视为 PIV 设备，并停止发现进程。
2. 如果命令失败，则会发出 SELECT 命令来查找 GID 辅助。 如果此命令成功，则 Windows 将该卡视为 GID 设备，并且发现进程将停止。
3. 如果命令失败，状态代码指示智能卡上没有任何帮助，则 Windows 仍会继续执行，就像卡是一个 GID 设备一样。 如果命令失败并出现任何其他错误，Windows 会将该卡视为未知设备。

## <a name="electrical-profile-for-gids-cards-with-the-microsoft-generic-profile"></a>带有 Microsoft 通用配置文件的 GID 卡的电气配置文件

对于实现 GID 卡边缘的智能卡，必须使用电气配置文件对其进行预配，使其能够使用收件箱类微型驱动程序进行设置。 本部分中的信息需要深入了解 GID 规范中指定的 Apdu、数据模型和卡边缘。

此处提供的子节必须按列出的顺序执行，然后才能将该卡用于个性化。 有关本部分中引用的 Apdu 的详细信息，请参阅 GID 规范的第11部分。

### <a name="gids-application-metadata"></a>GID 应用程序元数据

本节中所述的 DOs 由 GID 管理，只能在 SELECT 命令的响应数据字段中检索。 只有在应用程序处于 "创建" 状态时才能创建此元数据。 有关 GID 生命周期管理的详细信息，请参阅 GID 规范的第6节。

请注意，下面提供的元数据只包含完全按所述形式显示的内容，除非) 另外说明 (。 其他字段可能是可选的，也可能是智能卡应用程序供应商自定义的。

### <a name="file-control-information-df-fci"></a> (DF FCI) 的文件控制信息

|标记|Len|“值”|
|----|----|----|
|64|差.|应用程序模板数据对象</br></br>标记</br>4F</br>Len</br>差.</br>“值”</br>应用程序辅导 =</br></br>A0 00 00 03 97 42 54 46 59 xx yy</br><ul><li>**XX** = gid 规范修订号，即01或02。</li><li>**YY** = 为卡应用程序保留。</li></ul>|

### <a name="file-management-data-df-fmd"></a>文件管理数据 (DF FMD) 

|标记|Len|“值”|
|----|----|----|
|64|差.|FMD 模板</br></br>标记</br>5F2F</br>Len</br>差.</br>“值”</br>PIN 使用策略 (参阅 "PIN 使用策略" ) =</br></br>40或60<ul><li>**40** –应用程序 PIN 存在，可用于满足 CHV。</li><li>**60** -应用程序和全局 pin 均存在，可用于满足 CHV。</li></ul>|

### <a name="file-control-parameters-df-fcp"></a>文件控制参数 (DF FCP) 

|标记|Len|“值”|
|----|----|----|
|62|差.|FCP 模板</br></br>标记</br>82</br>Len</br>01</br>“值”</br>文件描述符字节： 38 ( "不能共享的 DF" ) </br></br>标记</br>8C</br>Len</br>03</br>“值”</br>精简格式的安全属性 =</br></br>03 30 30</br><ul><li>**40** -以下字节指定为 EFS 创建文件的要求，并按顺序)  (的删除文件。</li><li>**60** –用户身份验证或外部身份验证满足创建 EFs 的要求。</li><li>**60** –用户身份验证或外部身份验证满足删除 EFs 的要求。</li></ul>
<div class="alert">
<strong>注意</strong>  安全属性不必与此完全匹配，但允许用户身份验证或外部身份验证创建和删除 EFs。
</div>|

创建 DF FCP 后，该卡会转换为 "初始化" 状态，这是创建以下部分中所列的对象所需的状态。

### <a name="pin-creation"></a>创建 PIN

若要创建 PIN，必须将应用程序密码的更改引用数据 APDU 发送到卡：

**CLA**：00

**INS**：24

**P1**：01

**P2**：80

**Lc**：命令数据字段的长度

**数据字段**： &lt; 密码&gt;

**Le**：不存在

例如，若要将 PIN 设置为12345678，必须将以下 APDU 发送到卡：

``` syntax
00 24 01 80 08 31 32 33 34 35 36 37 38
```

### <a name="pin-unblock-key-puk-creation"></a>固定解锁密钥 (PUK) 创建

如果卡被阻止或忘记了 PIN，则使用 PUK 来取消阻止和/或重置 PIN。 如果改为使用管理密钥质询/响应，请不要创建 PUK。

若要创建 PUK，必须将应用程序重置密码的更改引用数据 APDU 发送到卡：

**CLA**：00

**INS**：24

**P1**：01

**P2**：81

**Lc**：命令数据字段的长度

**数据字段**： &lt; 密码&gt;

**Le**：不存在

例如，若要将 PUK 设置为12345678，则必须将以下 APDU 发送到卡：

``` syntax
00 24 01 81 08 31 32 33 34 35 36 37 38
```

### <a name="acl-creation"></a>创建 ACL

必须使用 "创建文件" APDU 创建 Acl：

**CLA**：00

**INS**： E0

**P1-P2**： 00 00

**Lc**：数据字段的长度

**数据字段**： EF 的 FCP 模板

**Le**：不存在

必须创建下表中所述的 Acl。 每个 ACL 创建 APDU 必须后跟 ActivateFile APDU (00 44 00 00 00) 

| ACL| APDU|
|-----|----|
| UserCreateDeleteDirAc    | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 00 8C 03 03 30 00 |
| EveryoneReadUserWriteAc  | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 10 8C 03 03 30 00 |
| UserWriteExecuteAc       | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 11 8C 03 03 30 FF |
| EveryoneReadAdminWriteAc | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 12 8C 03 03 20 00 |
| UserReadWriteAc          | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 13 8C 03 03 30 30 |
| AdminReadWriteAc         | 00 E0 00 00 0E 62 0C 82 01 39 83 02 A0 14 8C 03 03 20 20 |

### <a name="create-ef-for-admin-key"></a>为管理密钥创建 EF

必须使用 "创建文件" APDU 创建 EF for Admin key：

**CLA**：00

**INS**： E0

**P1-P2**： 00 00

**Lc**：数据字段的长度

**数据字段**： EF 的 FCP 模板 (EFID = B080，KeyID = 80) 

**Le**：不存在

必须将以下 APDU 发送到卡，才能为三重 DES 三密钥管理密钥创建 EF：

``` syntax
00 E0 00 00 1C 62 1A 82 01 18 83 02 B0 80 8C 04 87 00 20 FF A5 0B A4 09 80 01 02 83 01 80 95 01 C0
```

上面提到的命令必须后跟 ActivateFile APDU：

``` syntax
00 44 00 00 00
```

### <a name="inject-admin-key"></a>插入管理密钥

必须使用 PUT 键 APDU 将管理密钥注入到卡上：

**CLA**：00

**INS**： DB

**P1-P2**： 3F FF

**Lc**：数据字段的长度

**数据字段**：密钥用法模板

**Le**：不存在

必须将以下 APDU 发送到卡，才能将管理密钥注入到 KeyID 80：

``` syntax
00 DB 3F FF 26 70 24 84 01 80 A5 1F 87 18 01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08 01 02
03 04 05 06 07 08 88 03 B0 73 DC
```

在上述示例中，将用以下值注入管理密钥：

``` syntax
01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08 01 02 03 04 05 06 07 08
```

### <a name="set-operational-state"></a>设置操作状态

若要将卡从 "初始化" 状态转换为 "操作" 状态，则需要将包含 EFID 的选择 DF 发送到智能卡。

首先，为 DF 发送 SELECT APDU：

**CLA**：00

**INS**： A4

**P1-P2**： 00 0C

**Lc**：02

**数据字段**： 3F FF

**Le**：不存在

其次，使用 "激活文件" APDU 将 DF 的状态更改为 "操作"：

**CLA**：00

**INS**：44

**P1-P2**： 00 00

**Lc**：00

**数据字段**：不存在

**Le**：不存在

必须将以下 APDU 发送到卡，才能使其进入操作状态：

``` syntax
00 A4 00 0C 02 3F FF
00 44 00 00 00
```

完成此步骤后，该卡就可以根据 "文件系统规范" 一节中所述放置文件系统，并将其视为 "空白卡"。 按照 "创建" 卡上的步骤使用微型驱动程序 API 将文件系统置于卡上。 或者，按照下一部分中的步骤操作，使用 Apdu 将文件系统放在卡片上。

### <a name="data-objects-on-a-gids-card-after-the-filesystem-is-created"></a>创建文件系统后，GID 卡上的数据对象

对于与带有 Microsoft 通用配置文件的 GID 规范兼容的卡，下表介绍了在创建必需对象之后，按 "创建" 一节中的数据对象及其相应的 EFIDs。 如果未使用微型驱动程序 API 来创建文件系统，请使用在 GID 规范中指定的 "PUT DATA" APDU，将下表中的每个数据对象置于卡片上。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">EFID</th>
<th align="left">DO 标记</th>
<th align="left">目录</th>
<th align="left">友好名称</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">A000</td>
<td align="left">DF1F</td>
<td align="left"><pre class="syntax" space="preserve"><code>01 6d 73 63 70 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 a0 00 00 00 00 00
00 00 00 00 00 00 63 61 72 64 69 64 00 00 00 00
00 20 df 00 00 12 a0 00 00 00 00 00 00 00 00 00
00 00 63 61 72 64 61 70 70 73 00 00 00 21 df 00
00 10 a0 00 00 00 00 00 00 00 00 00 00 00 63 61
72 64 63 66 00 00 00 00 00 22 df 00 00 10 a0 00
00 6d 73 63 70 00 00 00 00 00 63 6d 61 70 66 69
6c 65 00 00 00 23 df 00 00 10 a0 00 00</code></pre></td>
<td align="left">主文件系统表</td>
</tr>
<tr class="even">
<td align="left">A010</td>
<td align="left">DF21</td>
<td align="left"><pre class="syntax" space="preserve"><code>6d 73 63 70 00 00 00 00</code></pre></td>
<td align="left">\cardapps</td>
</tr>
<tr class="odd">
<td align="left">A010</td>
<td align="left">DF22</td>
<td align="left"><pre class="syntax" space="preserve"><code>00 00 00 00 00 00</code></pre></td>
<td align="left">\cardcf</td>
</tr>
<tr class="even">
<td align="left">A010</td>
<td align="left">DF23</td>
<td align="left"><pre class="syntax" space="preserve"><code>&lt;empty 0-byte data object&gt;</code></pre></td>
<td align="left">mscp\cmapfile</td>
</tr>
<tr class="odd">
<td align="left">A012</td>
<td align="left">DF20</td>
<td align="left"><pre class="syntax" space="preserve"><code>&lt;random 16-byte value&gt;</code></pre></td>
<td align="left">\cardid</td>
</tr>
</tbody>
</table>

## <a name="inf-sample-to-re-brand-inbox-class-minidriver"></a>用于重新标记收件箱类微型驱动程序的 INF 示例

智能卡供应商可以使用收件箱微型驱动程序，而无需交付驱动程序包。 为了将品牌信息添加到此类卡的即插即用体验中，供应商可以提供用于重写各种字符串以提供品牌信息的 INF 文件。 这些字符串包括：

- ProviderName
- CardDeviceName
- SmartCardName

下面是可以与收件箱微型驱动程序一起使用的示例 INF 文件。 此 INF 文件在 x86 和 amd64 CPU 平台中进行了修饰。

``` syntax
;
;FabrikamVendor Smartcard Minidriver for an x86 and x64 based package.
;

[Version]
Signature="$Windows NT$"
Class=SmartCard
ClassGuid={990A2BD7-E738-46c7-B26F-1CF8FB9F1391}
Provider=%ProviderName%
CatalogFile=delta.cat
DriverVer=10/03/2009,10.0.0.1

[Manufacturer]
%ProviderName%=Minidriver,NTamd64,NTamd64.6.1,NTx86,NTx86.6.1

[Minidriver.NTamd64]
%CardDeviceName%=Minidriver64_Install,SCFILTER\CID_51FF0800

[Minidriver.NTx86]
%CardDeviceName%=Minidriver32_Install,SCFILTER\CID_51FF0800

[Minidriver.NTamd64.6.1]
%CardDeviceName%=Minidriver64_61_Install,SCFILTER\CID_51FF0800

[Minidriver.NTx86.6.1]
%CardDeviceName%=Minidriver32_61_Install,SCFILTER\CID_51FF0800

[DefaultInstall]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[DefaultInstall.ntamd64]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[DefaultInstall.NTx86]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[DefaultInstall.ntamd64.6.1]
AddReg=AddRegWOW64
AddReg=AddRegDefault

[DefaultInstall.NTx86.6.1]
AddReg=AddRegDefault

[SourceDisksFiles]
msclmd64.dll=1
msclmd.dll=1

[SourceDisksNames]
1 = %MediaDescription%

[Minidriver64_Install.NT]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[Minidriver64_61_Install.NT]
AddReg=AddRegWOW64
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[Minidriver32_Install.NT]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[Minidriver32_61_Install.NT]
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[Minidriver64_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services

[Minidriver32_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services


[Minidriver64_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[Minidriver64_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[Minidriver64_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[Minidriver32_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[Minidriver32_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[Minidriver32_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[amd64_CopyFiles]
msclmd.dll,msclmd64.dll

[x86_CopyFiles]
msclmd.dll

[wow64_CopyFiles]
msclmd.dll

[AddRegWOW64]
HKLM, %SmartCardNameWOW64%,"ATR",0x00000001,3b,04,51,ff,08,00
HKLM, %SmartCardNameWOW64%,"ATRMask",0x00000001,ff,ff,ff,ff,ff,ff
HKLM, %SmartCardNameWOW64%,"Crypto Provider",0x00000000,"Microsoft Base Smart Card Crypto Provider"
HKLM, %SmartCardNameWOW64%,"Smart Card Key Storage Provider",0x00000000,"Microsoft Smart Card Key Storage Provider"
HKLM, %SmartCardNameWOW64%,"80000001",0x00000000,%SmartCardCardModule%

[AddRegDefault]
HKLM, %SmartCardName%,"ATR",0x00000001,3b,04,51,ff,08,00
HKLM, %SmartCardName%,"ATRMask",0x00000001,ff,ff,ff,ff,ff,ff
HKLM, %SmartCardName%,"Crypto Provider",0x00000000,"Microsoft Base Smart Card Crypto Provider"
HKLM, %SmartCardName%,"Smart Card Key Storage Provider",0x00000000,"Microsoft Smart Card Key Storage Provider"
HKLM, %SmartCardName%,"80000001",0x00000000,%SmartCardCardModule%

[DestinationDirs]
amd64_CopyFiles=10,system32
x86_CopyFiles=10,system32
wow64_CopyFiles=10,syswow64


; =================== Generic ==================================

[Strings]
ProviderName ="FabrikamVendor"
MediaDescription="FabrikamVendor Smart Card Minidriver Installation Disk"
CardDeviceName="FabrikamVendor Minidriver for Smart Card"
SmartCardName="SOFTWARE\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardNameWOW64="SOFTWARE\Wow6432Node\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardCardModule="msclmd.dll"
```

对于这种类型的 INF 文件，需要满足以下要求：

- % FabrikamCardDeviceName% 字符串指定的硬件 ID 必须是设备的 ATR 历史字节或设备的智能卡框架标识符的已解码值。 有关此标识符的详细信息，请参阅 [发现过程](discovery-process.md)中的 "Windows 智能卡框架标识符" 部分。
- **DefaultInstall** 节是适用于智能卡微型驱动程序包的 INF 文件中的必需部分。
- INF 文件中的 **DriverVer** 指令的值必须大于收件箱驱动程序的 INF 文件中的版本和时间戳值。 否则，系统不会使用供应商的 INF 文件来安装设备。

    **DriverVer** 指令具有以下语法。

    ``` syntax
    DriverVer=mm/dd/yyyy[,w.x.y.z]
    ```

    建议你在设置 **DriverVer** 指令的值时遵循以下准则：

  - 指定一个最适合未来的日期值，以避免与 Windows Service Pack 更新冲突。
  - 尽管4位数版本号是可选的，但你必须指定比收件箱驱动程序的 INF 文件中指定的当前版本明显更高的版本。

有关 INF 文件和语法的详细信息，请参阅 [设备和驱动程序安装设计指南](../install/overview-of-device-and-driver-installation.md)。
