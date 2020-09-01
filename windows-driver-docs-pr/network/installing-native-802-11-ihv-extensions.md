---
title: 安装本机 802.11 IHV 扩展
description: 安装本机 802.11 IHV 扩展
ms.assetid: 73e45572-6f48-43da-9456-4de5e1f1901f
keywords:
- IHV 扩展 WDK 本机802.11，安装
- 安装本机 802.11 IHV 扩展
- 本机 802.11 IHV 扩展 WDK，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4370c75e2bebc4a61d32f656ddb901a40d896c0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218077"
---
# <a name="installing-native-80211-ihv-extensions"></a>安装本机 802.11 IHV 扩展




 

若要安装 [本机 802.11 Ihv 扩展 dll](native-802-11-ihv-extensions-dll4.md) 和 [本机 802.11 IHV UI 扩展 dll](native-802-11-ihv-ui-extensions-dll2.md)，独立硬件供应商 (IHV) 必须对 INF 文件中用于安装 IHV 的无线 LAN (WLAN) 适配器的 DDInstall 部分进行以下更改。

-   向 INF 文件添加一个带有关联的 *文件列表部分*的 CopyFiles 指令。 IHV 开发的每个 DLL 的名称必须在 *文件列表部分*内。

    例如，如果 IHV 正在 IhvExt.dll 和 IhvUIExt.dll 中安装，则 INF 文件将包含以下 CopyFiles 指令和 *文件列表部分*：

    ```
    CopyFiles = Sample-File-List-Section

    [Sample-File-List-Section]
    IhvExt.dll,,,2
    IhvUIExt.dll,,,2
    ```

    有关 CopyFiles 指令的详细信息，请参阅 [**INF CopyFiles 指令**](../install/inf-copyfiles-directive.md)。

-   请确保 DestinationDirs 部分声明了 CopyFiles 指令中使用的 *文件列表节* 的目标。

    在上面的示例中，DestinationDirs 节具有以下值：

    ```
    [DestinationDirs]
    DefaultDestDir = 11
    Sample-File-List-Section = 11
    ```

    有关 DestinationDirs 部分的详细信息，请参阅 [**INF DestinationDirs 部分**](../install/inf-destinationdirs-section.md)。

-   确保向每个 WLAN 适配器的 INF 文件中添加了一个带有关联的 " *添加注册表" 部分*的 AddReg 指令。 有关 AddReg 指令的详细信息，请参阅 [**INF AddReg 指令**](../install/inf-addreg-directive.md)。

    在 " *添加注册表" 部分*中，必须声明以下项。

    <a href="" id="hkr--ndi-ihvextensions--extensibilitydll--0----------destination-file-name"></a>HKR、Ndi \\ IHVExtensions、ExtensibilityDLL、0、 *destination-name*  
    此密钥标识 IHV 扩展 DLL 的名称。 例如，若要将 IhvExt.dll 与 WLAN 适配器的管理相关联，则将声明以下注册表项。

    ```
    HKR,Ndi\IHVExtensions, ExtensibilityDLL, 0, %SystemRoot%\system32\IhvExt.dll
    ```

    <a href="" id="hkr--ndi-ihvextensions--uiextensibilityclsid--0----------clsid"></a>HKR、Ndi \\ IHVExtensions、UIExtensibilityCLSID、0、 *CLSID*  
    此密钥标识 (CLSID) 的 COM 类标识符，该标识符是在 IHV UI 扩展 DLL 的目标系统上注册的。 *CLSID*值必须用引号引起来。 此密钥将 IHV UI 扩展 DLL 与通过 **ExtensibilityDLL** 密钥安装的 IHV 扩展 dll 关联起来。

    **注意**   仅当 IHV 安装 IHV UI 扩展 DLL 时，才需要**UIExtensibilityCLSID**项。

     

    <a href="" id="hkr--ndi-ihvextensions--adapteroui--0x00010001----------oui"></a>HKR、Ndi \\ IHVExtensions、AdapterOUI、0x00010001、 *OUI*  
    此密钥用于标识 (OUI) 的、用于标识 IHV 的 IEEE 分配的组织唯一标识符。 OUI 值必须声明为24位十六进制值。

    AdapterOUI 键用于验证 WLAN 适配器的 OUI 是否与**IHV** XML 元素的**oui**属性的值相匹配。 有关 **IHV** 元素和本机 802.11 XML 架构的详细信息，请参阅 Microsoft Windows SDK 文档。

有关 INF 文件及其部分的详细信息，请参阅 [创建 Inf 文件](../install/overview-of-inf-files.md)。

 

 