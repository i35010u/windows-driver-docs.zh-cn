---
title: 智能卡即插
description: 智能卡即插
ms.assetid: AE65A450-62A4-4774-A935-B7CB4301CCF4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f2e345399fd9a7b0e885b2bb3bf7979198543d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520629"
---
# <a name="smart-card-plug-and-play"></a>智能卡即插


## <a name="span-idpairingprocessspanspan-idpairingprocessspanspan-idpairingprocessspan-pairing-process"></a><span id="_Pairing_Process"></span><span id="_pairing_process"></span><span id="_PAIRING_PROCESS"></span> 配对过程


操作系统执行下列步骤以对智能卡与已安装的微型驱动程序：

-   从智能卡获取的 ATR。
-   循环访问项中 HKEY\_本地\_机\\软件\\Microsoft\\加密\\Calais\\智能卡注册表键，执行以下操作：

    -   应用到从智能卡已获取的 ATR 注册表中存储的 ATRMask 子密钥值。
    -   为存储在注册表的 ATR 子项值已掩码的 ATR 值进行比较。
    -   如果两个 ATR 值匹配，停止处理，并对相应与智能卡微型驱动程序。

智能卡 ATR 和 ATRMask 值必须是精心挑选，用于避免错误配对使用智能卡微型驱动程序。 存储在注册表中的智能卡 ATR 值后 ATRMask 已应用于从智能卡中读取的 ATR 应预期值。 否则为从卡和注册表已掩码的 ATR 值不匹配，配对失败。

开始使用 Windows 7 中，第一次智能卡插入到搜索 Windows Update 站点上相应微型驱动程序会导致卡读取器触发插事件。 若要在 Windows Update 上找到的驱动程序将 Windows 生成的设备 ID 取决于以下因素：

-   ATR 历史字节。 有关 ATR 历史字节的详细信息，请参阅标准 ISO/IEC 7816-4:2005(E) 的第 8 节。
-   中有一个列表的 GUID 标记 0x7F68 Microsoft Plug and Play 帮助应用程序状态。
-   这将与收件箱驱动程序配对的卡上的 PIV 应用程序存在。
-   GID （通用标识设备规范） 上的应用程序与 Microsoft 的泛型配置文件将与收件箱驱动程序配对卡存在。

有关更多详细信息插和 Winscard 的智能卡发现过程，请参阅[智能卡发现过程](discovery-process.md)。 这些进程导致的智能卡的唯一设备 ID 生成。

**请注意**  ，确定 Windows 生成的智能卡的设备 ID，建议的方法是在附加到正在运行 Windows 7 或更高版本的 Windows 的计算机的智能卡读卡器中插入智能卡。 然后可以通过查看智能卡设备在设备管理器的"硬件 Id"属性找到设备 ID。

 

## <a name="span-idsampleinfforx86andamd64spanspan-idsampleinfforx86andamd64spanspan-idsampleinfforx86andamd64spansample-inf-for-x86-and-amd64"></a><span id="Sample_INF_for_x86_and_amd64"></span><span id="sample_inf_for_x86_and_amd64"></span><span id="SAMPLE_INF_FOR_X86_AND_AMD64"></span>用于 x86 和 amd64 示例 INF


下面是智能卡安装在 Windows 8 和 Windows 的早期版本中的示例 INF 文件。 此 INF 文件安装在 X86 和 AMD64 CPU 平台进行了修饰。

**请注意**  若要避免部署问题，我们强烈建议对测试在全新安装之前提交 Winqual 的驱动程序包中所有目标的操作系统的驱动程序包。

 

``` syntax
;
;FabrikamVendor Smartcard Minidriver for an x86 and x64 based package.
;

[Version]
Signature="$Windows NT$"
Class=SmartCard
ClassGuid={990A2BD7-E738-46c7-B26F-1CF8FB9F1391}
Provider=%FABRIKAMVENDOR%
CatalogFile=delta.cat
DriverVer=10/03/2008,7.0.0.4

[Manufacturer]
%FABRIKAMVENDOR%=FabrikamVendor,NTamd64,NTamd64.6.1,NTx86,NTx86.6.1

[FabrikamVendor.NTamd64]
%FabrikamCardDeviceName%=FabrikamVendor64_Install,SCFILTER\CID_51FF0800

[FabrikamVendor.NTx86]
%FabrikamCardDeviceName%=FabrikamVendor32_Install,SCFILTER\CID_51FF0800

[FabrikamVendor.NTamd64.6.1]
%FabrikamCardDeviceName%=FabrikamVendor64_61_Install,SCFILTER\CID_51FF0800

[FabrikamVendor.NTx86.6.1]
%FabrikamCardDeviceName%=FabrikamVendor32_61_Install,SCFILTER\CID_51FF0800

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

[SourceDisksFiles]
Fabrikamcm64.dll=1
Fabrikamcm.dll=1

[SourceDisksNames]
1 = %MediaDescription%

[FabrikamVendor64_Install.NT]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault

[FabrikamVendor64_61_Install.NT]
CopyFiles=amd64_CopyFiles
CopyFiles=wow64_CopyFiles
AddReg=AddRegWOW64
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[FabrikamVendor32_Install.NT]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault

[FabrikamVendor32_61_Install.NT]
CopyFiles=x86_CopyFiles
AddReg=AddRegDefault
Include=umpass.inf
Needs=UmPass

[FabrikamVendor64_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services

[FabrikamVendor32_61_Install.NT.Services]
Include=umpass.inf
Needs=UmPass.Services


[FabrikamVendor64_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[FabrikamVendor64_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[FabrikamVendor64_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[FabrikamVendor32_61_Install.NT.HW]
Include=umpass.inf
Needs=UmPass.HW

[FabrikamVendor32_61_Install.NT.CoInstallers]
Include=umpass.inf
Needs=UmPass.CoInstallers


[FabrikamVendor32_61_Install.NT.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces


[amd64_CopyFiles]
Fabrikamcm.dll,Fabrikamcm64.dll

[x86_CopyFiles]
Fabrikamcm.dll

[wow64_CopyFiles]
Fabrikamcm.dll

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
FABRIKAMVENDOR ="FabrikamVendor"
MediaDescription="FabrikamVendor Smart Card Minidriver Installation Disk"
FabrikamCardDeviceName="FabrikamVendor Minidriver for Smart Card"
SmartCardName="SOFTWARE\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardNameWOW64="SOFTWARE\Wow6432Node\Microsoft\Cryptography\Calais\SmartCards\Fabrikam"
SmartCardCardModule="Fabrikamcm.dll"
```

此类型的 INF 文件需要以下项：

-   由 %fabrikamcarddevicename%字符串必须 ATR 历史字节的设备或设备的智能卡框架标识符的已解码的值指定硬件 ID。 有关此标识符的详细信息，请参阅智能卡发现过程中的"Windows 智能卡框架卡标识符"部分。
-   DefaultInstall 部分针对智能卡微型驱动程序的包的 INF 文件中是必需的。

 

 





