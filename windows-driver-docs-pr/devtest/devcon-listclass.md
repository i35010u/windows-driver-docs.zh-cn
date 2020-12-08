---
title: DevCon ListClass
description: 列出指定设备安装程序类中的所有设备。 在本地和远程计算机上有效。
keywords:
- DevCon ListClass 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon ListClass
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e88c900f73b21d0309d1ec1e2a3517b340e6275
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783377"
---
# <a name="devcon-listclass"></a>DevCon ListClass


列出指定设备安装程序类中的所有设备。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] listclass class [class...] 
```

## <a name="span-idddk_devcon_listclass_toolsspanspan-idddk_devcon_listclass_toolsspanparameters"></a><span id="ddk_devcon_listclass_tools"></span><span id="DDK_DEVCON_LISTCLASS_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span>**/m： \\ \\**<em>计算机</em>   
在指定的远程计算机上运行命令。 反斜杠是必需的。

**注意**   若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和 Windows 7 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问不可用。



<span id="_______class______"></span><span id="_______CLASS______"></span>*类*   
指定设备安装程序类。 不需要等号 (=) 。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M** 参数必须位于操作名称的前面 (**listclass**) 。 否则，DevCon 将忽略 **/m** 参数，并显示本地计算机上的设备，而不会返回语法错误。

安装程序类显示中的每个条目都代表一个设备。 该条目由唯一的实例名称和设备在 *实例* **：** *说明* 格式中的说明组成。

若要查找特定设备的安装类，请使用 [**DevCon Stack**](devcon-stack.md) 操作。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon listclass printers ports
devcon /m:\\Server01 listclass SmartCardReader
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例6：列出设备安装程序类中的设备](devcon-examples.md#ddk_example_6_list_the_devices_in_a_device_setup_class_tools)

[示例7：列出远程计算机上多个类中的设备](devcon-examples.md#ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute)









