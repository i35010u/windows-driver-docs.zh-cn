---
title: 要求安装另一个网络组件
description: 要求安装另一个网络组件
ms.assetid: 30e6db7f-46f4-414f-a485-051b007f0eb6
keywords:
- 添加注册表部分 WDK 网络连接、 组件依赖项
- 组件 Id WDK 网络
- 组件依赖项 WDK 网络
- 依赖项 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d5f02db5864cf9d3798f4021eee5a7e1c1094f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358393"
---
# <a name="requiring-the-installation-of-another-network-component"></a>要求安装另一个网络组件





网络组件可能需要一个或多个其他网络组件的安装才能正常运行。 网络 INF 文件指定了与每个此类依赖项**RequiredAll**值。 **RequiredAll**添加值 (通过*添加注册表部分*) 到**Ndi**密钥要求安装另一个网络的网络组件组件。

下面的示例演示**RequiredAll**中的条目*添加注册表部分*:

```INF
[ndi.reg]
HKR, Ndi, RequiredAll, 0, "component id"
```

*组件 ID*是*hw id*的所需的网络组件。 有关详细信息，请参阅[ **INF 模型部分**](https://msdn.microsoft.com/library/windows/hardware/ff547456)。 如果某个网络组件需要多个其他网络组件的安装，请使用一个**RequiredAll**条目为每个网络组件，必须安装，如下面的示例中所示：

```INF
HKR, Ndi, RequiredAll, 0, "component1 id, component2 id"
```

**请注意**   **RequiredAll**值仅应该用于安装隐藏不能由用户安装的网络组件。 此类组件应支持用户界面。 通过指定的组件的所有网络**RequiredAll**不能删除之前所需通过其安装的网络组件**RequiredAll**自行删除。

 

例如，如果 INF 文件组件的指定，通过**RequiredAll**，才删除组件 A，组件 B，组件 B 上的依赖项不能将其删除。 **RequiredAll**因此应安装绝对操作所需的另一个网络组件的网络组件。 例如，如果网络组件的 INF 文件 （适配器） 将使用**RequiredAll**若要指定必须安装了 tcp/ip 协议，用户将不能删除 TCP/IP 直到删除该适配器。 由于适配器不需要 TCP/IP 进行操作，不应使用的适配器 INF **RequiredAll**若要在 TCP/IP 上指定的依赖关系。

指定的 INF 文件**RequiredAll**依赖项必须确保所需的网络组件的 INF 文件是否存在 inf 目录中。 通常情况下，这通过实现**CopyINF**指令。 有关详细信息**CopyINF**指令，请参阅[ **INF CopyINF 指令**](https://msdn.microsoft.com/library/windows/hardware/ff547317)。 有关复制 INF 文件的详细信息，请参阅[复制 Inf](https://msdn.microsoft.com/library/windows/hardware/ff540117)。

如果指定的网络组件的安装，则**RequiredAll**条目失败，需要指定的组件也会失败的网络组件的安装。

 

 





