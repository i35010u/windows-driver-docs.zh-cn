---
title: INF 文件条目
description: INF 文件条目
ms.assetid: 8af2cbe7-f249-4e2f-940f-b50bc451cabe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06986259d2420fdffd29be15c989d406c0f26ef5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189159"
---
# <a name="inf-file-entries"></a>INF 文件条目





使用设备的 microdriver 需要 (INF) 文件的安装信息中的其他条目。 首先，INF 文件的 **DeviceData** 部分中必须有一个名为 "MicroDriver" 的条目。 有关详细信息，请 (参阅 [WIA 设备的 INF 文件](inf-files-for-wia-devices.md) 。 ) 此项应设置为实现 MICRODRIVER 的 DLL 的名称。

### <a name="windows-me-inf-file-entries"></a>Windows Me INF 文件条目

以下内容适用于 Microsoft Windows Millennium Edition (Me) 、Windows XP 和更高版本的操作系统。

在 [**Inf AddReg 指令**](../install/inf-addreg-directive.md) 中的空间（其中，WIA 微型驱动程序通常会被引用），inf 应作为驱动程序列出 *wiafbdrv.dll* 。 这是实现 WIA 平板驱动程序的组件。

请确保 [**INF CopyFiles 指令**](../install/inf-copyfiles-directive.md) 同时包含 microdriver 和 *wiafbdrv.dll*，这是从 Windows CAB 文件中复制的。 INF 文件的其余部分与其他 WIA 设备相同。

### <a name="windows-xp-inf-file-entries"></a>Windows XP INF 文件条目

以下信息适用于 Windows XP 和更高版本。 Windows Me INF 文件不使用 **Include** 和 **需要** 指令，因此不能使用这种类型的 inf。

[**INF DDInstall 部分**](../install/inf-ddinstall-section.md)应包含指令**Include**= sti。 此外， **需求** 指令应引用 **STI。MICRODRIVERSection**，以及相应的设备类型部分。 这会提供必要的 USDClass 和 CLSID **AddReg** 指令，因此不需要在 INF 中显式包含这些指令。

**注意**   不需要在**CopyFiles**指令中包含*wiafbdrv.dll* 。

 

Windows 驱动程序 (工具包上的 WIA microdriver 附带的 INF) CD 使用这一新方法来引用 microdriver。

 

