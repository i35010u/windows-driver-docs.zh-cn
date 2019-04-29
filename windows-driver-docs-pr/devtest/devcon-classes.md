---
title: DevCon Classes
description: 列出所有的设备安装程序类，包括在系统上的设备不使用的类。 在本地和远程计算机上有效。
ms.assetid: 05b9339c-30d1-45df-8f43-20a07e520a42
keywords:
- DevCon 类驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Classes
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76725660621ec94910d8931cfce7e5ab6446b7ba
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360115"
---
# <a name="devcon-classes"></a>DevCon Classes


列出所有[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)，包括在系统上的设备不使用的类。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] classes 
```

## <a name="span-idddkdevconclassestoolsspanspan-idddkdevconclassestoolsspanparameters"></a><span id="ddk_devcon_classes_tools"></span><span id="DDK_DEVCON_CLASSES_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\computer**   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问将不可用。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/M**参数必须在之前的操作名称 (**类**)。 否则，将忽略 DevCon **/m**参数，并显示不带返回语法错误的本地计算机上的类。

中的 DevCon 显示中，它们在注册表 （由 GUID 的字母数字顺序） 中显示的顺序列出类。

若要查找设备安装程序类中，使用[ **DevCon ListClass** ](devcon-listclass.md)操作。 若要查找特定设备的安装程序类，使用[ **DevCon 堆栈**](devcon-stack.md)操作。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon classes
devcon classes > setupclasses.txt
devcon /m:\\Server01 classes
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例 4:在本地计算机上的列表类](devcon-examples.md#ddk_example_4_list_classes_on_the_local_computer_tools)

[示例 5:在远程计算机上的列表类](devcon-examples.md#ddk_example_5_list_classes_on_the_remote_computer_tools)









