---
title: DevCon Update
description: 强制将指定的设备的当前设备驱动程序替换指定的 INF 文件中列出的驱动程序。 仅在本地计算机上有效。
ms.assetid: c07d7abe-31d8-4a8d-87da-8db649710c15
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
ms.openlocfilehash: c6a6eb4e267c054a8c9ae92008b2a67ac439f2db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371526"
---
# <a name="devcon-update"></a>DevCon Update


强制将指定的设备的当前设备驱动程序替换指定的 INF 文件中列出的驱动程序。 仅在本地计算机上有效。

```
    devcon [/r] update INFfile HardwareID 
```

## <a name="span-idddkdevconupdatetoolsspanspan-idddkdevconupdatetoolsspanparameters"></a><span id="ddk_devcon_update_tools"></span><span id="DDK_DEVCON_UPDATE_TOOLS"></span>参数


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件性重新启动。 完成操作，仅当必须重新启动，以使更改生效后，会重新启动系统。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span> *INFfile*   
指定此更新中使用的 INF （信息） 文件的完整路径和文件名。 如果省略路径，DevCon 假定该文件位于当前目录。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span> *HardwareID*   
使用指定的硬件 id。 更新设备驱动的程序 此命令中指定的硬件 ID 必须完全符合设备的硬件 ID。 模式不是有效的。 请不要键入一个单引号字符 (  ) 以指示文本值。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**DevCon 更新**操作强制更新到最合适的驱动程序中指定的 INF 文件，即使这些驱动程序是较旧或比当前驱动程序或不同的 INF 文件中的驱动程序不太合适。 有关详细信息，请参阅[安装程序如何选择驱动程序](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-selects-drivers)。

不能使用**DevCon 更新**命令以更新虚幻设备的驱动程序。

在更新之前，在任何设备的驱动程序确定哪些设备将受到 update 命令。 若要执行此操作，使用硬件 ID 在显示命令中，如[ **DevCon HwIDs** ](devcon-hwids.md)或[ **DevCon DriverFiles**](devcon-driverfiles.md)。 这一点尤其重要**DevCon 更新**操作因为 DevCon 不会列出它更新的设备驱动程序。

DevCon 提示用户如果 INF 文件指定未签名的驱动程序，或如果它找不到所需的文件，例如在可移动媒体上的驱动程序文件。 若要禁止显示需要响应提示，请使用非交互式更新操作中， [ **DevCon UpdateNI**](devcon-updateni.md)。

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，添加条件的重新启动参数 (/ r) 命令。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon update c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r update c:\windows\inf\newdvc.inf *PNP030b
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例 32:通信端口的驱动程序更新](devcon-examples.md#ddk_example_32_update_the_driver_for_communication_ports_tools)

[示例 44:强制更新 HAL](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)









