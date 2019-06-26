---
title: 安装本机 802.11 IHV 扩展
description: 安装本机 802.11 IHV 扩展
ms.assetid: 73e45572-6f48-43da-9456-4de5e1f1901f
keywords:
- IHV 扩展安装 WDK 本机 802.11
- 安装本机 802.11 IHV 扩展
- 本机 802.11 IHV 扩展 WDK 安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0714e63eabed796726839a84c60c32449a617ebf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385848"
---
# <a name="installing-native-80211-ihv-extensions"></a>安装本机 802.11 IHV 扩展




 

若要安装[本机 802.11 IHV 扩展 DLL](native-802-11-ihv-extensions-dll4.md)并[本机 802.11 IHV UI 扩展 DLL](native-802-11-ihv-ui-extensions-dll2.md)，独立硬件供应商 (IHV) 必须对 INF 的 DDInstall 部分进行以下更改用于 IHV 的无线 LAN (WLAN) 适配器的安装文件。

-   添加 CopyFiles 指令，且其关联*文件列表部分*，到 INF 文件。 由 IHV 开发的每个 DLL 的名称必须在*文件列表部分*。

    例如，如果 IHV 安装 IhvExt.dll 和 IhvUIExt.dll，INF 文件将具有以下 CopyFiles 指令和*文件列表部分*:

    ```
    CopyFiles = Sample-File-List-Section

    [Sample-File-List-Section]
    IhvExt.dll,,,2
    IhvUIExt.dll,,,2
    ```

    有关 CopyFiles 指令的详细信息，请参阅[ **INF CopyFiles 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)。

-   请确保 DestinationDirs 部分声明的目标*文件列表部分*CopyFiles 指令中使用。

    在上一示例中，DestinationDirs 部分将具有以下值：

    ```
    [DestinationDirs]
    DefaultDestDir = 11
    Sample-File-List-Section = 11
    ```

    有关 DestinationDirs 部分的详细信息，请参阅[ **INF DestinationDirs 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)。

-   请确保一个 AddReg 指令，且其关联*添加注册表部分*，添加到每个 WLAN 适配器的 INF 文件。 有关 AddReg 指令的详细信息，请参阅[ **INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

    内*添加注册表部分*，必须声明为以下项。

    <a href="" id="hkr--ndi-ihvextensions--extensibilitydll--0----------destination-file-name"></a>HKR、 Ndi\\IHVExtensions、 ExtensibilityDLL，0，*目标文件名*  
    此密钥标识 IHV 扩展 DLL 的名称。 例如，若要将 IhvExt.dll WLAN 适配器的管理与相关联，将声明以下项。

    ```
    HKR,Ndi\IHVExtensions, ExtensibilityDLL, 0, %SystemRoot%\system32\IhvExt.dll
    ```

    <a href="" id="hkr--ndi-ihvextensions--uiextensibilityclsid--0----------clsid"></a>HKR、 Ndi\\IHVExtensions、 UIExtensibilityCLSID，0， *CLSID*  
    此键标识的 COM 类标识符 (CLSID)，这为 IHV UI 扩展 DLL 在目标系统上注册。 *CLSID*值必须括在引号中。 此密钥将与通过安装 IHV 扩展 DLL 相关联 IHV UI 扩展 DLL **ExtensibilityDLL**密钥。

    **请注意**   **UIExtensibilityCLSID**密钥是必需的仅当 IHV 安装 IHV UI 扩展 DLL。

     

    <a href="" id="hkr--ndi-ihvextensions--adapteroui--0x00010001----------oui"></a>HKR、 Ndi\\IHVExtensions、 AdapterOUI，0x00010001， *OUI*  
    此键标识的 IEEE 分配组织唯一标识符 (OUI)，它标识 IHV。 OUI 值必须声明为 24 位十六进制值。

    AdapterOUI 密钥用于验证是否将 WLAN 适配器 OUI 与匹配的值**OUI**的属性**IHV** XML 元素。 有关详细信息**IHV**元素和本机 802.11 XML 架构，请参阅 Microsoft Windows SDK 文档。

INF 文件和其部分有关的详细信息，请参阅[创建一个 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)。

 

 





