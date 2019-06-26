---
title: DevCon ClassFilter
description: 添加、 删除、 显示和更改设备安装程序类的筛选器驱动程序的顺序。 仅在本地计算机上有效。
ms.assetid: c04200c7-2897-46bd-ac5f-f838efef79d9
keywords:
- DevCon ClassFilter 驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon ClassFilter
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4726de37587886cb63be71e39bbed603a3e5b709
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360368"
---
# <a name="devcon-classfilter"></a>DevCon ClassFilter


添加、 删除、 显示和更改设备安装程序类的筛选器驱动程序的顺序。 仅在本地计算机上有效。

```
    devcon classfilter class {upper | lower} [ = | @driver | -driver | +driver | !driver ]...
```

## <a name="span-idddkdevconclassfiltertoolsspanspan-idddkdevconclassfiltertoolsspanparameters"></a><span id="ddk_devcon_classfilter_tools"></span><span id="DDK_DEVCON_CLASSFILTER_TOOLS"></span>参数


<span id="_______class______"></span><span id="_______CLASS______"></span> *class*   
指定设备安装程序类。

<span id="_______upper______"></span><span id="_______UPPER______"></span> **upper**   
指示指定的驱动程序是大写类筛选器驱动程序。

<span id="_______lower______"></span><span id="_______LOWER______"></span> **lower**   
指示指定的驱动程序的较低类别筛选器驱动程序。

<span id="______________"></span> **=**    
将光标移到 （前面的第一个驱动程序） 的筛选器驱动程序列表的开头。

<span id="________driver______"></span><span id="________DRIVER______"></span> **@** <em>driver</em>   
将游标定位到指定的驱动程序的下一个实例上。

<span id="-driver"></span><span id="-DRIVER"></span>* *-***driver*  
添加之前。 将插入指定的驱动程序之前在其放置光标的驱动程序。

如果游标未定位的驱动程序，DevCon 列表的开始处插入指定的驱动程序。 子命令完成后，将光标置于新添加的驱动程序。

<span id="________driver______"></span><span id="________DRIVER______"></span> **+** <em>driver</em>   
将添加的后面。 后在其放置光标的驱动程序插入指定的驱动程序。

如果游标未定位的驱动程序，DevCon 在列表末尾插入指定的驱动程序。 子命令完成后，将光标置于新添加的驱动程序。

<span id="________driver______"></span><span id="________DRIVER______"></span> **!** <em>driver</em>   
从列表中删除指定的驱动程序的下一个匹配项。

子命令完成后，光标将占用已删除的驱动程序的位置。 后续 **+** 或 **-** 子命令在光标位置插入新的驱动程序。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

一个**DevCon ClassFilter**命令可以包含一个或多个运算符的包含的子命令 ( **=** ， **@** ，  **-** ， **+** ， **！** ) 和筛选器驱动程序名称。 DevCon 出现在命令中的顺序执行子命令。

而无需子命令， **DevCon ClassFilter**命令显示上限或下限的筛选器驱动程序中指定的类。 例如， **devcon classfilter net 低**显示较低的筛选器驱动程序中的净安装程序类。

**DevCon ClassFilter**操作使用虚拟游标的类的筛选器驱动程序列表中移动。 将光标从筛选器驱动程序，才能在列表中的第一个驱动程序的列表开头开始。 返回到起始位置，除非游标始终将向前移动通过筛选器驱动程序列表 DevCon 执行子命令。

除非驱动程序安装为服务 DevCon 不会向类添加筛选器驱动程序，即，必须有一个用于中的驱动程序的注册表子项[HKLM\\系统\\CurrentControlSet\\Services](https://docs.microsoft.com/windows-hardware/drivers/install/hklm-system-currentcontrolset-services-registry-tree)注册表项。 这种保护措施可防止意外添加筛选器驱动程序不存在，从而使系统无法启动。

由于筛选器驱动程序更改需要重新启动设备，使用[ **DevCon 重启**](devcon-restart.md)命令，或包括 **/r** 中的（条件重启）参数**DevCon ClassFilter**命令。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon classfilter mouse upper
devcon /r classfilter mouse upper !mouclass +newmou
devcon /r classfilter net lower @netfltr -testfltr
devcon /r classfilter volume upper !volsnap =!volsnap2
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 23:显示安装程序类的筛选器驱动程序](devcon-examples.md#ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools)

[示例是 24:将筛选器驱动程序添加到安装程序类](devcon-examples.md#ddk_example_24_add_a_filter_driver_to_a_setup_class_tools)

[示例 25:类列表中插入筛选器驱动程序](devcon-examples.md#ddk_example_25_insert_a_filter_driver_in_the_class_list_tools)

[示例 26:替换为筛选器驱动程序](devcon-examples.md#ddk_example_26_replace_a_filter_driver_tools)

[示例 27:更改筛选器驱动程序的顺序](devcon-examples.md#ddk_example_27_change_the_order_of_filter_drivers_tools)









