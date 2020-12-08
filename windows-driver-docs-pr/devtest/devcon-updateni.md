---
title: DevCon UpdateNI
description: 强制将当前设备驱动程序替换为指定 INF 文件中列出的驱动程序，而不提示用户提供信息或进行确认。 仅在本地计算机上有效。
keywords:
- DevCon UpdateNI 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon UpdateNI
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f73f398fc100d05567744b94b0c72b2916dbbc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783331"
---
# <a name="devcon-updateni"></a>DevCon UpdateNI


强制将当前设备驱动程序替换为指定 INF 文件中列出的驱动程序，而不提示用户提供信息或进行确认。 仅在本地计算机上有效。

```
    devcon [/r] updateni INFfile HardwareID 
```

## <a name="span-idddk_devcon_updateni_toolsspanspan-idddk_devcon_updateni_toolsspanparameters"></a><span id="ddk_devcon_updateni_tools"></span><span id="DDK_DEVCON_UPDATENI_TOOLS"></span>参数


<span id="________r______"></span><span id="________R______"></span>**/r**   
条件重启。 仅当需要重新启动才能使更改生效时，才能在完成操作后重新启动系统。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span>*INFfile*   
为设备指定 INF (信息) 的完整路径和文件名。 如果省略路径，则 DevCon 会假定文件位于当前目录中。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span>*HardwareID*   
指定设备的硬件 ID。

指定的硬件 ID 必须与设备的硬件 ID 完全匹配。 模式无效。 不要键入单引号字符 (**"**) 来指示文本值。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**DevCon UpdateNI** 操作取消了需要响应的所有用户提示，并假定默认响应。 因此，不能使用此操作来安装未签名的驱动程序。 若要在更新过程中显示用户提示，请使用 [**DevCon update**](devcon-update.md)。

**DevCon UpdateNI** 操作会强制进行更新，即使指定 INF 文件中的驱动程序比当前驱动程序更旧或更低。

更新任何设备的驱动程序之前，请确定将受更新命令影响的设备。 为此，请在显示命令中使用硬件 ID，如 [**DevCon hwid**](devcon-hwids.md) 或 [**devcon DriverFiles**](devcon-driverfiles.md)。 这在 **Devcon UpdateNI** 操作中尤其重要，因为 devcon 不会列出它所更新的设备驱动程序。

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，请将 (/r) 的条件重新启动参数添加到命令中。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon updateni c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r updateni c:\windows\inf\newdvc.inf *PNP030b
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例32：更新通信端口的驱动程序](devcon-examples.md#ddk_example_32_update_the_driver_for_communication_ports_tools)









