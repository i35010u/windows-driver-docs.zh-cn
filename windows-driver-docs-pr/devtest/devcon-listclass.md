---
title: DevCon ListClass
description: 列出指定的设备安装程序类中的所有设备。 在本地和远程计算机上有效。
ms.assetid: b642ca5e-5ef1-499f-b8c5-96583a4bd411
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
ms.openlocfilehash: 8f1e54a08ff250f896e401ac5b0f9743ac618e19
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543159"
---
# <a name="devcon-listclass"></a>DevCon ListClass


列出指定的设备安装程序类中的所有设备。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] listclass class [class...] 
```

## <a name="span-idddkdevconlistclasstoolsspanspan-idddkdevconlistclasstoolsspanparameters"></a><span id="ddk_devcon_listclass_tools"></span><span id="DDK_DEVCON_LISTCLASS_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\**<em>computer</em>   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问将不可用。



<span id="_______class______"></span><span id="_______CLASS______"></span> *class*   
指定设备安装程序类。 不带等号 （=） 是必需的。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/M**参数必须在之前的操作名称 (**listclass**)。 否则，将忽略 DevCon **/m**参数，并显示不带返回语法错误的本地计算机上的设备。

在安装程序类显示每个条目表示一台设备。 唯一的实例名称和说明中的设备的条目组成*实例* **:** *说明*格式。

若要查找特定设备的安装程序类，使用[ **DevCon 堆栈**](devcon-stack.md)操作。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon listclass printers ports
devcon /m:\\Server01 listclass SmartCardReader
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 6:设备安装程序类中的设备列表](devcon-examples.md#ddk_example_6_list_the_devices_in_a_device_setup_class_tools)

[示例 7:在远程计算机上的多个类的设备列表](devcon-examples.md#ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute)









