---
title: DevCon Reboot
description: 停止，然后启动操作系统。 仅在本地计算机上有效。
ms.assetid: 4e27c35c-8b98-4edc-98d7-8ba0f96d7a78
keywords:
- DevCon 重新启动驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Reboot
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92af29ce5dd13cb84d8eaff0ce5286ff1694d2da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347033"
---
# <a name="devcon-reboot"></a>DevCon Reboot


停止，然后启动操作系统。 仅在本地计算机上有效。

```
    devcon reboot 
```

## <span id="ddk_devcon_reboot_tools"></span><span id="DDK_DEVCON_REBOOT_TOOLS"></span>


### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

与不同 **/r**参数，它仅在需要以使更改生效，重新启动系统时， **DevCon 重启**操作会重新启动系统，而无需确定是否需要重新启动。

DevCon 使用标准**ExitWindowsEx**函数以重新启动。 如果用户已在计算机上打开的文件或程序将不会关闭，直到用户已答复了系统提示，关闭文件或结束该进程不重新启动系统。 有关详细信息**ExitWindowsEx**，请参阅 Microsoft Windows SDK。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon reboot
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例 39:重新启动本地计算机](devcon-examples.md#ddk_example_39_reboot_the_local_computer_tools)









