---
title: DevCon 安装
description: 创建新的、 根枚举的 devnode 非即插即用设备并安装其支持软件。 仅在本地计算机上有效。
ms.assetid: d31007dd-6f20-460d-8561-d1639c69aa09
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
ms.openlocfilehash: 122eab295ea09855ca4c49d77fc1fa899de59adf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542333"
---
# <a name="devcon-install"></a>DevCon 安装


创建新的、 根枚举的 devnode 非即插即用设备并安装其支持软件。 仅在本地计算机上有效。

```
    devcon [/r] install INFfile HardwareID 
```

## <a name="span-idddkdevconinstalltoolsspanspan-idddkdevconinstalltoolsspanparameters"></a><span id="ddk_devcon_install_tools"></span><span id="DDK_DEVCON_INSTALL_TOOLS"></span>参数


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件性重新启动。 完成操作时必须重新启动，以使更改生效后，会重新启动系统。 默认情况下，DevCon 不重新启动系统。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span> *INFfile*   
指定设备的 INF 文件的完整路径和文件名。 如果省略路径，DevCon 假定该文件位于当前目录。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span> *HardwareID*   
指定设备的硬件 ID。

指定的硬件 ID 必须完全符合设备的硬件 ID。 模式不是有效的。 请不要键入一个单引号字符 () 以指示文本值。 有关详细信息，请参阅[硬件 Id](https://msdn.microsoft.com/library/windows/hardware/ff546152)并[设备标识字符串](https://msdn.microsoft.com/library/windows/hardware/ff541224)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，添加条件的重新启动参数 (**/r**) 到该命令。

不能使用**DevCon 安装**插设备的操作。

**DevCon 安装**操作创建一个新的非即插设备节点。 然后，它使用[ **DevCon 更新**](devcon-update.md)操作以安装新添加的设备驱动程序。 因此，成功消息**DevCon 安装**操作报告 DevCon 已创建设备节点，并且它已更新设备的驱动程序。

如果任何步骤**DevCon 安装**操作将失败，DevCon 显示失败消息，并会继续进行驱动程序安装。

**DevCon 安装**命令创建一个新的非即插设备节点每次运行它。 若要更新或重新安装驱动程序，请使用[ **DevCon 更新**](devcon-update.md)命令。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon install c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r install c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 33:安装设备](devcon-examples.md#ddk_example_33_install_a_device_tools)

[示例 34:安装使用无人参与的安装的设备](devcon-examples.md#ddk_example_34_install_a_device_using_unattended_setup_tools)

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[硬件 Id](https://msdn.microsoft.com/library/windows/hardware/ff546152)

[设备标识字符串](https://msdn.microsoft.com/library/windows/hardware/ff541224)










