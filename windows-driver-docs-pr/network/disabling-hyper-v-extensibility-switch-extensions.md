---
title: 禁用 Hyper-V 可扩展交换机扩展
description: 禁用 Hyper-V 可扩展交换机扩展
ms.assetid: 3BE5A53E-3F74-4B99-B504-5D7F090343E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 127545ed7e06c7ade1c4eaa635c7136f25ec71e8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217638"
---
# <a name="disabling-hyper-v-extensible-switch-extensions"></a>禁用 Hyper-V 可扩展交换机扩展


[VMSwitchExtension](/powershell/module/hyper-v/disable-vmswitchextension) PowerShell cmdlet 在可扩展交换机的特定实例上禁用扩展。

[VMSwitchExtension](/powershell/module/hyper-v/disable-vmswitchextension) cmdlet 使用以下语法：

``` syntax
Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-ComputerName <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitchName] <string[]> [-ComputerName
    <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitch] <VMSwitch[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtension] <VMSwitchExtension[]> [-ComputerName <string[]>]
    [<CommonParameters>]
```

下面演示了如何使用 [VMSwitchExtension](/powershell/module/hyper-v/disable-vmswitchextension) cmdlet 的示例。

``` syntax
PS C:\Windows\system32> Disable-VMSwitchExtension "Switch Extensibility Test Extension 1" PrivateNetwork

PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork "Switch Extensibility Test Extension 1" | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False
```

## <a name="related-topics"></a>相关主题


[VMSwitchExtension](/powershell/module/hyper-v/disable-vmswitchextension)

[VMSwitchExtension](/powershell/module/hyper-v/get-vmsystemswitchextension)

[**Msvm \_ EthernetSwitchExtension**](/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

 

