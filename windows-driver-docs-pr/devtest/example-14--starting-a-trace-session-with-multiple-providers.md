---
title: 示例使用多个提供程序启动跟踪会话的 14
description: 示例使用多个提供程序启动跟踪会话的 14
ms.assetid: fda63107-608c-4278-abf8-1447c8f8302a
keywords:
- Tracelog WDK，提供程序
- 提供程序 WDK 软件跟踪
- 跟踪 WDK，提供程序
- 多个提供程序 WDK 软件跟踪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 496a596b75df6c98adcd9808b1ba3a5a50ec9e89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344692"
---
# <a name="example-14-starting-a-trace-session-with-multiple-providers"></a>示例 14：使用多个提供程序启动跟踪会话


## <span id="ddk_starting_a_session_with_multiple_providers_tools"></span><span id="DDK_STARTING_A_SESSION_WITH_MULTIPLE_PROVIDERS_TOOLS"></span>


以下命令使用两个跟踪提供程序启动跟踪会话：

```
tracelog -start MyTraces -guid 2guids.guid -f mytraces.etl
```

该命令看起来像标准**tracelog-开始**命令，但指定的文件**guid**参数、 2guids.guid，包含以下两个提供程序 Guid （每行一个），如以下示例所示：

```
1540ff4c-3fd7-4bba-9938-1d1bf31573a7
dab01d4d-2d48-477d-b1c3-daad0ce6f06b
```

在提交此命令时，Tracelog 启动与两个提供程序的单个跟踪会话，让这两个提供程序。

提供程序共享跟踪缓冲区和事件跟踪日志 (.etl) 文件。 从每个提供程序的跟踪消息混杂在跟踪日志中。 任何标志和命令中指定的级别应用于所有提供程序中跟踪会话。

若要验证是否已启用这两个跟踪提供程序，请使用**tracelog enumguid**命令，如以下命令中所示。

```
tracelog -enumguid
```

在响应中，跟踪日志显示向 ETW 注册提供程序的列表，并显示了其中两个启用。 已启用提供程序显示为粗体文本显示。

```
c:\Tracelog>tracelog -enumguid
##     Guid                       Enabled  LoggerId Level Flags
------------------------------------------------------------
1046d4b1-fce5-48bc-8def-fd33196af19a     FALSE  0    0    0
4a8aaa94-cfc4-46a7-8e4e-17bc45608f0a     FALSE  0    0    0
196e57d9-49c0-4b3b-ac3a-a8a93ada1938     FALSE  0    0    0
1540ff4c-3fd7-4bba-9938-1d1bf31573a7      TRUE  2    0    0
f12b1984-4c42-11d3-ab7b-00c04f68fcdc     FALSE  0    0    0
1fbecc45-c060-4e7c-8a0e-0dbd6116181b     FALSE  0    0    0
94a984ef-f525-4bf1-be3c-ef374056a592     FALSE  0    0    0
3121cf5d-c5e6-4f37-be86-57083590c333     FALSE  0    0    0
fc4b0d39-e8be-4a83-a32f-c0c7c4f61ee4     FALSE  0    0    0
fc570986-5967-4641-a6f9-05291bce66c5     FALSE  0    0    0
39a7b5e0-be85-47fc-b9f5-593a659abac1     FALSE  0    0    0
dab01d4d-2d48-477d-b1c3-daad0ce6f06b      TRUE  2    0    0k
bca7bd7f-b0bf-4051-99f4-03cfe79664c1     FALSE  0    0    0
d58c126f-b309-11d1-969e-0000f875a5bc     FALSE  0    0    0
d58c126e-b309-11d1-969e-0000f875a5bc     FALSE  0    0    0
58db8e03-0537-45cb-b29b-597f6cbebbfe     FALSE  0    0    0
27246e9d-b4df-4f20-b969-736fa49ff6ff     FALSE  0    0    0
```

若要在会话中的每个跟踪提供程序指定不同的标志和级别，使用单独**tracelog-启用**命令对于每个提供程序，如以下命令中所示。

```
tracelog -enable MyTraces -guid #1540ff4c-3fd7-4bba-9938-1d1bf31573a7 -flag 2 -level 1
tracelog -enable MyTraces -guid #dab01d4d-2d48-477d-b1c3-daad0ce6f06b -flag 3 -level ffff
```

 

 





