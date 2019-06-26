---
title: 枚举 Hyper-V 可扩展交换机扩展
description: 枚举 Hyper-V 可扩展交换机扩展
ms.assetid: AC468A8F-5C48-419B-9E9E-D63925E1CE9D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 477799f927ef067e391b71dc79d1b7c4f153171d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354581"
---
# <a name="enumerating-hyper-v-extensible-switch-extensions"></a>枚举 Hyper-V 可扩展交换机扩展


[Get-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension) PowerShell cmdlet 枚举当前绑定到实例的可扩展交换机的 HYPER-V 可扩展交换机扩展插件。 此 cmdlet 还会报告扩展是否已启用可扩展交换机实例中。

[Get-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension) cmdlet 使用以下语法：

``` syntax
Get-VMSwitchExtension [[-VMSwitchName] <string[]>] [[-Name] <string[]>] [-ComputerName <string[]>]
    [<CommonParameters>]

Get-VMSwitchExtension [[-VMSwitch] <VMSwitch[]>] [-ComputerName <string[]>] [<CommonParameters>]
```

下面的示例演示的输出[Get-vmswitchextension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension) cmdlet。

``` syntax
PS C:\Windows\system32> Get-VMSwitchExtension PrivateNetwork | fl -property @("Name","ExtensionType", "SwitchName","Enabled")

Name          : NDIS Capture LightWeight Filter
ExtensionType : Capture
SwitchName    : PrivateNetwork
Enabled       : False

Name          : Switch Extensibility Test Extension 2
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False

Name          : Switch Extensibility Test Extension 1
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : False

Name          : WFP extensible switch Layers LightWeight Filter
ExtensionType : Filter
SwitchName    : PrivateNetwork
Enabled       : True
```

**请注意**  为了最小化信息的量，该示例通过管道通过筛选器命令"fl"将返回的扩展对象。 这将导致与的特性相匹配的要显示的信息子集 **-属性**切换。

 

## <a name="related-topics"></a>相关主题


[Get-VMSwitchExtension](https://docs.microsoft.com/powershell/module/hyper-v/get-vmsystemswitchextension)

[**Msvm\_EthernetSwitchExtension**](https://docs.microsoft.com/windows/desktop/HyperV_v2/msvm-ethernetswitchextension)

 

 






