---
title: 禁用 HYPER-V 可扩展交换机扩展
description: 禁用 HYPER-V 可扩展交换机扩展
ms.assetid: 3BE5A53E-3F74-4B99-B504-5D7F090343E5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b24381583612412642f2566e274f192b1497874b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544481"
---
# <a name="disabling-hyper-v-extensible-switch-extensions"></a>禁用 HYPER-V 可扩展交换机扩展


[Disable-vmswitchextension](https://technet.microsoft.com/library/hh848545.aspx) PowerShell cmdlet 可禁用可扩展交换机的特定实例中的扩展。

[Disable-vmswitchextension](https://technet.microsoft.com/library/hh848545.aspx) cmdlet 使用以下语法：

``` syntax
Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-ComputerName <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitchName] <string[]> [-ComputerName
    <string[]>] [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtensionName] <string[]> [-VMSwitch] <VMSwitch[]> [-ComputerName <string[]>]
    [<CommonParameters>]

Disable-VMSwitchExtension [-VMSwitchExtension] <VMSwitchExtension[]> [-ComputerName <string[]>]
    [<CommonParameters>]
```

下面演示了如何使用的示例[Disable-vmswitchextension](https://technet.microsoft.com/library/hh848545.aspx) cmdlet。

``` syntax
PS C:\Windows\system32> Disable-VMSwitchExtension "Switch Extensibility Test Extension 1" PrivateNetwork

PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork "Switch Extensibility Test Extension 1" | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False
```

## <a name="related-topics"></a>相关主题


[Disable-VMSwitchExtension](https://technet.microsoft.com/library/hh848545.aspx)

[Get-VMSwitchExtension](https://technet.microsoft.com/library/hh848603.aspx)

[**Msvm\_EthernetSwitchExtension**](https://msdn.microsoft.com/library/hh850139)

 

 






