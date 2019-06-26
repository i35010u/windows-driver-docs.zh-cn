---
title: 禁用 Hyper-V 可扩展交换机扩展
description: 禁用 Hyper-V 可扩展交换机扩展
ms.assetid: 3BE5A53E-3F74-4B99-B504-5D7F090343E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: adea2e584806ecd34629958dd88da2a20c066dbc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386569"
---
# <a name="disabling-hyper-v-extensible-switch-extensions"></a>禁用 Hyper-V 可扩展交换机扩展


[Disable-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/disable-vmswitchextension) PowerShell cmdlet 可禁用可扩展交换机的特定实例中的扩展。

[Disable-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/disable-vmswitchextension) cmdlet 使用以下语法：

``` syntax
Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-ComputerName <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitchName] <string[]> [-ComputerName
    <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitch] <VMSwitch[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtension] <VMSwitchExtension[]> [-ComputerName <string[]>]
    [<CommonParameters>]
```

下面演示了如何使用的示例[Disable-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/disable-vmswitchextension) cmdlet。

``` syntax
PS C:\Windows\system32> Disable-VMSwitchExtension "Switch Extensibility Test Extension 1" PrivateNetwork

PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork "Switch Extensibility Test Extension 1" | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False
```

## <a name="related-topics"></a>相关主题


[Disable-VMSwitchExtension](https://docs.microsoft.com/powershell/module/hyper-v/disable-vmswitchextension)

[Get-VMSwitchExtension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension)

[**Msvm\_EthernetSwitchExtension**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

 

 






