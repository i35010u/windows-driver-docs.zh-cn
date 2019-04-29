---
title: 处理不可用的符号存储
description: 处理不可用的符号存储
ms.assetid: 42e3518b-b139-49cd-96cc-ea31f6df7964
keywords:
- SymProxy，不可用的存储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 838b9e52c1bb27d61bb4a250201fe58face94809
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374913"
---
# <a name="dealing-with-unavailable-symbol-stores"></a>处理不可用的符号存储


如果其中一个符号存储 SymSrv 被配置为获取文件从故障或不可，结果可以是为每个文件请求从客户端长时间等待。 当从 SymProxy 调用 SymSrv 时，可以通过设置 SymSrv 停止尝试访问应用商店相关避免大部分这些等待。 当参与此功能时，SymSrv 停止尝试将存储用于一段时间后在设定的间隔期间可以体验指定的数量的超时从相同的存储区。 通过在.ini 文件或注册表中，可以控制这些变量的值。

**若要控制使用.ini 文件的符号存储区访问**

1.  在 %WINDIR%\\system32\\inetsrv\\Symsrv.ini，创建一个名为部分**超时**。

2.  添加值**触发器**，**计数**，并**中断**到此部分。

**触发器**指示以分钟为单位要监视的超时时间量。 **计数**指示的超时期间查找次数**触发器**段。 **中断**指示以分钟为单位来禁用存储在达到阈值后的时间长度。

例如，建议使用以下设置：

```ini
[timeouts]
trigger=10
count=5
blackout=15
```

在此示例中，如果在 10 分钟内遇到五个超时是商店访问权限被关闭状态。 在 15 分钟中断完成时，应用商店会重新激活。

**若要控制使用注册表的符号存储区访问**

1.  创建名为

    ```text
    HKLM\ Software\Microsoft\Symbol Server\Timeouts
    ```

2.  添加三个 REG\_DWORD 值**触发器**，**计数**，并且**中断**于此密钥。 像在.ini 文件中设置这些值。

是否使用注册表或.ini 文件，如果任何触发器、 计数或中断值设置为 0 或不存在任何键或值，此功能被禁用。

SymSrv 此功能目前仅在作为服务运行时。 这意味着此功能仅适合应用程序从 SymProxy 调用时。

 

 





