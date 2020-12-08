---
title: 智能卡即插即用
description: 智能卡即插即用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8d04979f7e845bb87ce99530d5dddc7f7394074
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811881"
---
# <a name="smart-card-plug-and-play"></a>智能卡即插即用


## <a name="span-id_pairing_processspanspan-id_pairing_processspanspan-id_pairing_processspan-pairing-process"></a><span id="_Pairing_Process"></span><span id="_pairing_process"></span><span id="_PAIRING_PROCESS"></span> 配对过程


操作系统遵循以下步骤，将智能卡与已安装的微型驱动程序配对：

-   从智能卡中获取 ATR。
-   循环访问 HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ 加密 \\ Calais \\ 智能卡注册表项中的条目，然后执行以下操作：

    -   将注册表中存储的 ATRMask 子项值应用到从智能卡获取的 ATR。
    -   将屏蔽的 ATR 值与注册表中存储的 ATR 子项值进行比较。
    -   如果两个 ATR 值匹配，则停止处理并将相应的微型驱动程序与智能卡配对。

必须仔细选择智能卡 ATR 和 ATRMask 值，以避免与智能卡的微型驱动程序错误配对。 将 ATRMask 应用于从智能卡中读取的 ATR 后，存储在注册表中的智能卡 ATR 值应是预期值。 否则，卡和注册表中的屏蔽 ATR 值不匹配，并且配对会失败。

从 Windows 7 开始，首次将智能卡插入读卡器时，将触发即插即用事件，这些事件会导致在 Windows 更新站点上搜索相应的微型驱动程序。 Windows 生成的用于在 Windows 更新上查找驱动程序的设备 ID 取决于以下因素：

-   ATR 中的历史字节数。 有关 ATR 历史字节的详细信息，请参阅 ISO/IEC 7816-4:2005 (E) 标准的第8部分。
-   Microsoft 即插即用辅助应用程序存在，其中包含标记0x7F68 中的 GUID 列表。
-   卡上存在 PIV 应用程序，该应用程序将与收件箱驱动程序配对。
-   存在一个 GID (通用标识设备规范) 使用 Microsoft 通用配置文件的应用程序，该卡将与收件箱驱动程序配对。

有关即插即用和 Winscard 的智能卡发现过程的更多详细信息，请参阅 [智能卡发现进程](discovery-process.md)。 这些过程会为智能卡生成唯一的设备 ID。

**注意**  若要确定 Windows 为智能卡生成的设备 ID，推荐的方法是将智能卡插入到连接到运行 Windows 7 或更高版本 Windows 的计算机的智能卡读卡器中。 然后，可以通过查看设备管理器中智能卡设备的 "硬件 Id" 属性来找到设备 ID。

 

## <a name="span-idsample_inf_for_x86_and_amd64spanspan-idsample_inf_for_x86_and_amd64spanspan-idsample_inf_for_x86_and_amd64spansample-inf-for-x86-and-amd64"></a><span id="Sample_INF_for_x86_and_amd64"></span><span id="sample_inf_for_x86_and_amd64"></span><span id="SAMPLE_INF_FOR_X86_AND_AMD64"></span>适用于 x86 和 amd64 的示例 INF


下面是 Windows 8 和早期版本的 Windows 中用于智能卡安装的示例 INF 文件。 此 INF 文件在 X86 和 AMD64 CPU 平台中进行了修饰。

**注意**  若要避免部署问题，强烈建议在将驱动程序包提交到 Winqual 之前，在所有目标操作系统的全新安装上测试驱动程序包。

 

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

对于这种类型的 INF 文件，需要满足以下要求：

-   % FabrikamCardDeviceName% 字符串指定的硬件 ID 必须是设备的 ATR 历史字节或设备的智能卡框架标识符的已解码值。 有关此标识符的详细信息，请参阅智能卡发现过程中的 "Windows 智能卡框架标识符" 部分。
-   DefaultInstall 节是适用于智能卡微型驱动程序包的 INF 文件中的必需部分。

 

 





