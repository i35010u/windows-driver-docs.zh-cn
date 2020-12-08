---
title: DevCon Update
description: 强制用指定 INF 文件中列出的驱动程序替换指定设备的当前设备驱动程序。 仅在本地计算机上有效。
keywords:
- DevCon 更新驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Update
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9836510abd6127d2db00ada22c12f3e87b1cfbf8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783339"
---
# <a name="devcon-update"></a>DevCon Update


强制用指定 INF 文件中列出的驱动程序替换指定设备的当前设备驱动程序。 仅在本地计算机上有效。

```
    devcon [/r] update INFfile HardwareID 
```

## <a name="span-idddk_devcon_update_toolsspanspan-idddk_devcon_update_toolsspanparameters"></a><span id="ddk_devcon_update_tools"></span><span id="DDK_DEVCON_UPDATE_TOOLS"></span>参数


<span id="________r______"></span><span id="________R______"></span>**/r**   
条件重启。 仅当需要重新启动才能使更改生效时，才能在完成操作后重新启动系统。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span>*INFfile*   
指定更新中使用 (信息) 文件的完整路径和文件名。 如果省略路径，则 DevCon 会假定文件位于当前目录中。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span>*HardwareID*   
更新具有指定硬件 ID 的设备的驱动程序。 此命令中指定的硬件 ID 必须与设备的硬件 ID 完全匹配。 模式无效。 不要键入单引号字符 (**"**) 来指示文本值。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

对于指定的 INF 文件中最合适的驱动程序， **DevCon update** 操作将强制进行更新，即使这些驱动程序比当前驱动程序或不同 INF 文件中的驱动程序更早或更低。 有关详细信息，请参阅 [安装程序如何选择驱动程序](../install/how-windows-selects-a-driver-for-a-device.md)。

不能使用 **DevCon update** 命令更新 nonpresent 设备的驱动程序。

更新任何设备的驱动程序之前，请确定将受更新命令影响的设备。 为此，请在显示命令中使用硬件 ID，如 [**DevCon hwid**](devcon-hwids.md) 或 [**devcon DriverFiles**](devcon-driverfiles.md)。 这在 **Devcon 更新** 操作中尤其重要，因为 devcon 不会列出它所更新的设备驱动程序。

如果 INF 文件指定了未签名的驱动程序，或者如果找不到所需的文件（如可移动介质上的驱动程序文件），则 DevCon 会提示用户。 若要取消需要响应的提示，请使用非交互式更新操作 [**UpdateNI**](devcon-updateni.md)。

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，请将 (/r) 的条件重新启动参数添加到命令中。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon update c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r update c:\windows\inf\newdvc.inf *PNP030b
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例32：更新通信端口的驱动程序](devcon-examples.md#ddk_example_32_update_the_driver_for_communication_ports_tools)

[示例44：强制更新 HAL](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)
