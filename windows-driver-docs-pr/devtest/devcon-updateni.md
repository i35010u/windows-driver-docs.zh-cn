---
title: DevCon UpdateNI
description: 强制将当前的设备驱动程序替换而不提示用户输入信息或进行确认指定的 INF 文件中列出的驱动程序。 仅在本地计算机上有效。
ms.assetid: 436a9731-1c61-4b38-b145-7012da55b699
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
ms.openlocfilehash: d059242dd4129a38c7052712e0c32fb08de9bc12
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567175"
---
# <a name="devcon-updateni"></a>DevCon UpdateNI


强制将当前的设备驱动程序替换而不提示用户输入信息或进行确认指定的 INF 文件中列出的驱动程序。 仅在本地计算机上有效。

```
    devcon [/r] updateni INFfile HardwareID 
```

## <a name="span-idddkdevconupdatenitoolsspanspan-idddkdevconupdatenitoolsspanparameters"></a><span id="ddk_devcon_updateni_tools"></span><span id="DDK_DEVCON_UPDATENI_TOOLS"></span>参数


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件性重新启动。 完成操作，仅当必须重新启动，以使更改生效后，会重新启动系统。

<span id="_______INFfile______"></span><span id="_______inffile______"></span><span id="_______INFFILE______"></span> *INFfile*   
指定设备 INF （信息） 文件的完整路径和文件名。 如果省略路径，DevCon 假定该文件位于当前目录。

<span id="_______HardwareID______"></span><span id="_______hardwareid______"></span><span id="_______HARDWAREID______"></span> *HardwareID*   
指定设备的硬件 ID。

指定的硬件 ID 必须完全符合设备的硬件 ID。 模式不是有效的。 请不要键入一个单引号字符 () 以指示文本值。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**DevCon UpdateNI**操作取消需要响应的所有用户提示，并假定默认响应。 因此，此操作不能用于安装未签名驱动程序。 若要在更新期间显示用户提示，请使用[ **DevCon 更新**](devcon-update.md)。

**DevCon UpdateNI**操作强制更新，即使指定的 INF 文件中的驱动程序是较旧或比当前驱动程序不太合适。

在更新之前，在任何设备的驱动程序确定哪些设备将受到 update 命令。 若要执行此操作，使用硬件 ID 在显示命令中，如[ **DevCon HwIDs** ](devcon-hwids.md)或[ **DevCon DriverFiles**](devcon-driverfiles.md)。 这一点尤其重要**DevCon UpdateNI**操作因为 DevCon 不会列出它更新的设备驱动程序。

系统可能需要重新启动才能使此更改生效。 若要让 DevCon 重新启动系统，添加条件的重新启动参数 (/ r) 命令。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon updateni c:\windows\inf\newdvc.inf ISAPNP\CSC4324\0
devcon /r updateni c:\windows\inf\newdvc.inf *PNP030b
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例 32:通信端口的驱动程序更新](devcon-examples.md#ddk_example_32_update_the_driver_for_communication_ports_tools)









