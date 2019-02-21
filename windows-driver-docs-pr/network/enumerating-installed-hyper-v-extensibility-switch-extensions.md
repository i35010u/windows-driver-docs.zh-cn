---
title: 枚举的 HYPER-V 可扩展交换机扩展
description: 枚举的 HYPER-V 可扩展交换机扩展
ms.assetid: AC468A8F-5C48-419B-9E9E-D63925E1CE9D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06c2019cdc8ce75135a6fa279d48573bc0132432
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554531"
---
# <a name="enumerating-hyper-v-extensible-switch-extensions"></a>枚举的 HYPER-V 可扩展交换机扩展


[Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx) PowerShell cmdlet 枚举当前绑定到实例的可扩展交换机的 HYPER-V 可扩展交换机扩展插件。 此 cmdlet 还会报告扩展是否已启用可扩展交换机实例中。

[Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx) cmdlet 使用以下语法：

``` syntax
Get-VMSwitchExtension [[-VMSwitchName] <string[]>] [[-Name] <string[]>] [-ComputerName <string[]>]
    [<CommonParameters>]

Get-VMSwitchExtension [[-VMSwitch] <VMSwitch[]>] [-ComputerName <string[]>] [<CommonParameters>]
```

下面的示例演示的输出[Get-vmswitchextension](https://technet.microsoft.com/library/hh848603.aspx) cmdlet。

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


[Get-VMSwitchExtension](https://technet.microsoft.com/library/hh848603.aspx)

[**Msvm\_EthernetSwitchExtension**](https://msdn.microsoft.com/library/hh850139)

 

 






