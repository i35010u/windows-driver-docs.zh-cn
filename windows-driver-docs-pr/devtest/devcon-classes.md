---
title: DevCon Classes
description: 列出了所有设备安装程序类，包括系统上的设备不使用的类。 在本地和远程计算机上有效。
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
ms.openlocfilehash: 888750dff0fbd22150a6f1e24b31da9bfc63fd61
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817813"
---
# <a name="devcon-classes"></a>DevCon Classes


列出了所有 [设备安装程序类](../install/overview-of-device-setup-classes.md)，包括系统上的设备不使用的类。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] classes 
```

## <a name="span-idddk_devcon_classes_toolsspanspan-idddk_devcon_classes_toolsspanparameters"></a><span id="ddk_devcon_classes_tools"></span><span id="DDK_DEVCON_CLASSES_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span>**/m： \\ \\计算机**   
在指定的远程计算机上运行命令。 反斜杠是必需的。

**注意**   若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和 Windows 7 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问不可用。



### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M** 参数必须位于)  (**类** 的操作名称之前。 否则，DevCon 将忽略 **/m** 参数，并在本地计算机上显示类，而不会返回语法错误。

在 DevCon 显示中，按 GUID) 的顺序列出类，按它们在 (注册表中的显示顺序列出。

若要在安装程序类中查找设备，请使用 [**DevCon ListClass**](devcon-listclass.md) 操作。 若要查找特定设备的安装类，请使用 [**DevCon Stack**](devcon-stack.md) 操作。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon classes
devcon classes > setupclasses.txt
devcon /m:\\Server01 classes
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

[示例4：在本地计算机上列出类](devcon-examples.md#ddk_example_4_list_classes_on_the_local_computer_tools)

[示例5：列出远程计算机上的类](devcon-examples.md#ddk_example_5_list_classes_on_the_remote_computer_tools)
