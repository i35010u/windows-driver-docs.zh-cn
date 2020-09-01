---
title: 要求安装另一个网络组件
description: 要求安装另一个网络组件
ms.assetid: 30e6db7f-46f4-414f-a485-051b007f0eb6
keywords:
- 添加-注册表--WDK 网络，组件依赖项
- 组件 Id WDK 网络
- 组件依赖项 WDK 网络
- 依赖项 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8341e3e669e3d6b865c230ddc693ab8138a1792a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215078"
---
# <a name="requiring-the-installation-of-another-network-component"></a>要求安装另一个网络组件





网络组件可能需要安装一个或多个其他网络组件，才能正常工作。 网络 INF 文件使用 **RequiredAll** 值指定每个此类依赖项。 将 **RequiredAll** 值添加 (通过) *添加* 到需要安装其他网络组件的网络组件的 **Ndi** 键。

以下示例显示了 "*添加注册表" 部分*中的**RequiredAll**条目：

```INF
[ndi.reg]
HKR, Ndi, RequiredAll, 0, "component id"
```

*组件 id*是所需的网络组件的*硬件 id* 。 有关详细信息，请参阅 [**INF 模型部分**](../install/inf-models-section.md)。 如果网络组件需要安装多个其他网络组件，请为每个必须安装的网络组件使用一个 **RequiredAll** 条目，如以下示例中所示：

```INF
HKR, Ndi, RequiredAll, 0, "component1 id, component2 id"
```

**注意**   **RequiredAll**值只应用于安装用户无法安装的隐藏网络组件。 此类组件不应支持用户界面。 在需要通过**RequiredAll**安装的网络组件本身被删除之前，不能删除由**RequiredAll**指定的任何网络组件。

 

例如，如果组件 A 的 INF 文件指定通过 **RequiredAll**，则在删除组件 a 之前，无法删除组件 b 上的依赖关系。 因此， **RequiredAll**应仅安装在另一个网络组件的操作中绝对需要的网络组件。 例如，如果网络组件的 INF 文件 (适配器) 使用 **RequiredAll** 指定必须安装 tcp/ip，则在删除该适配器之前，用户将无法删除 tcp/ip。 由于适配器不要求 TCP/IP 运行，因此适配器的 INF 不应使用 **RequiredAll** 来指定 tcp/ip 上的依赖关系。

指定 **RequiredAll** 依赖项的 inf 文件必须确保 inf 目录中存在所需的网络组件的 inf 文件。 通常，这是通过 **CopyINF** 指令来完成的。 有关 **CopyINF** 指令的详细信息，请参阅 [**INF CopyINF 指令**](../install/inf-copyinf-directive.md)。 有关复制 INF 文件的详细信息，请参阅 [复制 inf](../install/copying-inf-files.md)。

如果安装 **RequiredAll** 条目指定的网络组件失败，则需要指定组件的网络组件的安装也会失败。

 

