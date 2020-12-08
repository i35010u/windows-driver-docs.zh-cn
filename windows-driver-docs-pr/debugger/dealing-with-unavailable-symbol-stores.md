---
title: 处理不可用的符号存储
description: 处理不可用的符号存储
keywords:
- SymProxy，不可用的存储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87eac8cfcfbafc061235192079a7a783adef0c4d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823445"
---
# <a name="dealing-with-unavailable-symbol-stores"></a>处理不可用的符号存储


如果将 SymSrv 配置为从其获取文件的某个符号存储区已关闭或不可用，则结果可能会等待每个文件请求的客户端长时间等待。 从 SymProxy 调用 SymSrv 时，可以通过设置 SymSrv 来停止尝试访问有问题的应用程序，从而避免大多数这些等待。 使用此功能时，SymSrv 会在设定的时间间隔内，停止尝试使用存储的一段时间，在该时间段内发生指定数量的超时时间。 可以通过 .ini 文件或注册表控制这些变量的值。

**使用 .ini 文件控制符号存储区访问**

1.  在% WINDIR% \\ system32 \\ inetsrv \\Symsrv.ini 中，创建一个名为 **超时** 的部分。

2.  向此部分添加值 " **触发器**"、" **计数**" 和 " **中断** "。

**触发器** 表示监视超时所需的时间（分钟）。 **Count** 指示 **触发器** 期间要查找的超时数。 "**中断**" 指示达到阈值后禁用存储的时间长度（以分钟为单位）。

例如，建议采用以下设置：

```ini
[timeouts]
trigger=10
count=5
blackout=15
```

在此示例中，如果在10分钟的时间内遇到5次超时，则会关闭存储访问。 在15分钟的中断完成后，将重新激活存储区。

**使用注册表控制符号存储区访问**

1.  创建名为

    ```text
    HKLM\ Software\Microsoft\Symbol Server\Timeouts
    ```

2.  将三个 REG \_ DWORD 值 " **触发器**"、" **计数**" 和 " **中断** " 添加到此密钥。 在 .ini 文件中设置这些值。

无论是使用注册表还是 .ini 文件，如果有任何触发器、计数或掉电值设置为0，或者任何键或值都不存在，则将禁用此功能。

只有作为服务运行时，SymSrv 的此功能才可用。 这意味着，仅当从 SymProxy 调用此功能时，才会实际应用此功能。

 

 





