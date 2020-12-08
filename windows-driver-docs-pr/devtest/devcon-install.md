---
title: DevCon Install
description: 为非即插即用设备创建一个新的根枚举 devnode，并安装其支持的软件。 仅在本地计算机上有效。
keywords:
- DevCon 安装驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Install
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c462cbf900aacb1395f0fc6ae6f2e63f52d96216
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783389"
---
# <a name="devcon-install"></a>DevCon Install


为非即插即用设备创建一个新的根枚举 devnode，并安装其支持的软件。 仅在本地计算机上有效。

```
    devcon [/r] install INFfile HardwareID 
```

## <a name="span-idddk_devcon_install_toolsspanspan-idddk_devcon_install_toolsspanparameters"></a><span id="ddk_devcon_install_tools"></span><span id="DDK_DEVCON_INSTALL_TOOLS"></span>参数


<span id="________r______"></span><span id="________R______"></span>**/r**   
条件重启。 完成操作后，如果需要重新启动才能使更改生效，则重新启动系统。 默认情况下，DevCon 不会重新启动系统。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span>*INFfile*   
为设备指定 INF 文件的完整路径和文件名。 如果省略路径，则 DevCon 会假定文件位于当前目录中。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span>*HardwareID*   
指定设备的硬件 ID。

指定的硬件 ID 必须与设备的硬件 ID 完全匹配。 模式无效。 不要键入单引号字符 (**"**) 来指示文本值。 有关详细信息，请参阅 [硬件 id](../install/hardware-ids.md) 和 [设备标识字符串](../install/device-identification-strings.md)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，请将 (**/r**) 的条件重新启动参数添加到命令中。

不能对即插即用设备使用 **DevCon 安装** 操作。

**DevCon 安装** 操作会创建新的非即插即用设备节点。 然后，它使用 [**DevCon Update**](devcon-update.md) 操作来为新添加的设备安装驱动程序。 因此， **Devcon 安装** 操作的成功消息会报告 devcon 已创建设备节点，并且已更新设备的驱动程序。

如果 **Devcon 安装** 操作的任何步骤失败，则 devcon 会显示失败消息，不会继续安装驱动程序。

在每次运行 **DevCon 安装** 命令时，它都会创建一个新的非即插即用设备节点。 若要更新或重新安装驱动程序，请使用 [**DevCon update**](devcon-update.md) 命令。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon install c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r install c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例33：安装设备](devcon-examples.md#ddk_example_33_install_a_device_tools)

[示例34：使用无人参与安装程序安装设备](devcon-examples.md#ddk_example_34_install_a_device_using_unattended_setup_tools)

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[硬件 Id](../install/hardware-ids.md)

[设备标识字符串](../install/device-identification-strings.md)
