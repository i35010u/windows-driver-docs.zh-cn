---
title: DevCon ClassFilter
description: 添加、删除、显示和更改设备安装程序类的筛选器驱动程序的顺序。 仅在本地计算机上有效。
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
ms.openlocfilehash: a66ef07713799450a0fea530c2972ffd4bffe9bb
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382921"
---
# <a name="devcon-classfilter"></a>DevCon ClassFilter


添加、删除、显示和更改设备安装程序类的筛选器驱动程序的顺序。 仅在本地计算机上有效。

```
    devcon classfilter class {upper | lower} [ = | @driver | -driver | +driver | !driver ]...
```

## <a name="span-idddk_devcon_classfilter_toolsspanspan-idddk_devcon_classfilter_toolsspanparameters"></a><span id="ddk_devcon_classfilter_tools"></span><span id="DDK_DEVCON_CLASSFILTER_TOOLS"></span>参数


<span id="_______class______"></span><span id="_______CLASS______"></span>*类*   
指定设备安装程序类。

<span id="_______upper______"></span><span id="_______UPPER______"></span>**上限**   
指示指定的驱动程序为高类筛选器驱动程序。

<span id="_______lower______"></span><span id="_______LOWER______"></span>**降低**   
指示指定的驱动程序是低类筛选器驱动程序。

<span id="______________"></span> **=**   
将光标移到 (第一个驱动程序) 之前的筛选器驱动程序列表的开头。

<span id="________driver______"></span><span id="________DRIVER______"></span>**@**<em>驱动程序</em>   
将光标定位在指定驱动程序的下一个实例上。

<span id="-driver"></span><span id="-DRIVER"></span>**-* * * 驱动程序*  
添加之前。 在游标所定位到的驱动程序之前插入指定的驱动程序。

如果游标未定位在驱动程序上，则 DevCon 会将指定的驱动程序插入到列表的开头。 子命令完成时，光标将定位在新添加的驱动程序上。

<span id="________driver______"></span><span id="________DRIVER______"></span>**+**<em>驱动程序</em>   
添加 after。 将指定的驱动程序插入到光标所在的驱动程序之后。

如果游标未定位在驱动程序上，则 DevCon 会将指定的驱动程序插入到列表的末尾。 子命令完成时，光标将定位在新添加的驱动程序上。

<span id="________driver______"></span><span id="________DRIVER______"></span>**!**<em>驱动程序</em>   
从列表中删除指定驱动程序的下一个匹配项。

子命令完成后，光标将占据已删除驱动程序的位置。 后续 **+** 或子 **-** 命令在光标位置插入新驱动程序。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**DevCon ClassFilter**命令可以包含一个或多个子命令，其中包含一个运算符 (**=** 、 **@** 、 **-** 、 **+** 、 **！**) 和一个筛选器驱动程序名称。 DevCon 按它们出现在命令中的顺序执行子命令。

在不使用子命令的情况下， **DevCon ClassFilter** 命令显示指定类中的筛选器驱动程序的上限或下限。 例如， **devcon classfilter net lower** 显示 net setup 类中的筛选器驱动程序。

**DevCon ClassFilter**操作使用虚拟游标来浏览类的筛选器驱动程序列表。 游标从筛选器驱动程序列表的开头开始，在列表中的第一个驱动程序之前。 除非返回到起始位置，否则光标始终在筛选器驱动程序列表中向前移动，因为 DevCon 会执行子命令。

DevCon 不向类添加筛选器驱动程序，除非该驱动程序安装为服务，即 [HKLM \\ SYSTEM \\ CurrentControlSet \\ Services](../install/hklm-system-currentcontrolset-services-registry-tree.md) 注册表项中必须存在该驱动程序的注册表子项。 此安全措施可防止意外添加不存在的筛选器驱动程序，从而导致系统无法启动。

由于筛选器驱动程序更改需要重启设备，因此请使用[**Devcon Restart**](devcon-restart.md)命令，或在**devcon ClassFilter**命令中包含 **/r** (条件重启) 参数。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon classfilter mouse upper
devcon /r classfilter mouse upper !mouclass +newmou
devcon /r classfilter net lower @netfltr -testfltr
devcon /r classfilter volume upper !volsnap =!volsnap2
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例23：显示安装程序类的筛选器驱动程序](devcon-examples.md#ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools)

[示例24：向安装程序类添加筛选器驱动程序](devcon-examples.md#ddk_example_24_add_a_filter_driver_to_a_setup_class_tools)

[示例25：在类列表中插入筛选器驱动程序](devcon-examples.md#ddk_example_25_insert_a_filter_driver_in_the_class_list_tools)

[示例26：替换筛选器驱动程序](devcon-examples.md#ddk_example_26_replace_a_filter_driver_tools)

[示例27：更改筛选器驱动程序的顺序](devcon-examples.md#ddk_example_27_change_the_order_of_filter_drivers_tools)