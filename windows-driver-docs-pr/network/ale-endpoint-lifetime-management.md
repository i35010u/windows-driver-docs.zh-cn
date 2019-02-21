---
title: ALE 终结点生存期管理
description: ALE 终结点生存期管理
ms.assetid: cbf54062-4ced-4cf6-babf-e9e4e1ddf302
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976ac66dc1e0bc436cfc464d5ad940d54b9afc79
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522349"
---
# <a name="ale-endpoint-lifetime-management"></a>ALE 终结点生存期管理


支持应用程序层强制措施 (ALE) 标注驱动程序可能需要分配资源来处理的指示。 本主题介绍如何配置标注驱动程序关联的终结点关闭时释放此类资源。 Windows 7 和更高版本的 Windows 中支持 ALE 终结点生存期管理。

若要管理的 ALE 终结点相关联的资源，标注驱动程序可以注册以下层：

-   FWPS\_LAYER\_ALE\_RESOURCE\_RELEASE\_V4 (FWPM\_LAYER\_ALE\_RESOURCE\_RELEASE\_V4)

-   FWPS\_LAYER\_ALE\_RESOURCE\_RELEASE\_V6 (FWPM\_LAYER\_ALE\_RESOURCE\_RELEASE\_V6)

-   FWPS\_LAYER\_ALE\_ENDPOINT\_CLOSURE\_V4 (FWPM\_LAYER\_ALE\_ENDPOINT\_CLOSURE\_V4)

-   FWPS\_LAYER\_ALE\_ENDPOINT\_CLOSURE\_V6 (FWPM\_LAYER\_ALE\_ENDPOINT\_CLOSURE\_V6)

为在相应的 ALE 资源分配层的每个可能指示 ALE 资源发布层 (例如，FWPS\_层\_ALE\_资源\_分配\_V4)。 若要确保该标注驱动程序可以匹配到分配层 FWPS 版本层\_元数据\_字段\_传输\_终结点\_层和每个提供句柄的元数据字段终结点被分配唯一的句柄。

具体取决于终结点的类型以不同的方式调用 ALE 终结点闭包层。 对于 TCP 连接，ALE 终结点闭包所指示，对于每个 ALE 授权连接层 (例如 FWPS\_层\_ALE\_身份验证\_CONNECT\_V4) 或 ALE 授权接收接受 （适用于的层示例 FWPS\_层\_ALE\_身份验证\_收到\_接受\_V4) 指示。 与 ALE 资源发布迹象，引擎将分配唯一的句柄，每个终结点，并将其传递在 FWPS\_元数据\_字段\_传输\_终结点\_句柄的元数据字段。 对于非 TCP 终结点，无论包含几个唯一远程对等节点与套接字进行通信的每个终结点调用 ALE 终结点闭包层。 为每个 TCP 侦听套接字，ALE 终结点闭包层也会调用。

标注为 ALE 终结点闭包层注册可以挂起分类。 此标注以 reinject 任何数据包排队等待异步处理之前终结点关闭的情况下启用。 挂起分类到标注驱动程序必须调用[ **FwpsPendClassify0** ](https://msdn.microsoft.com/library/windows/hardware/ff551197)对的调用后跟[ **FwpsCompleteClassify0** ](https://msdn.microsoft.com/library/windows/hardware/ff551150)时处理已完成。

如果适用，则引擎将指示 FWPS 中的父终结点的唯一句柄\_元数据\_字段\_父\_终结点\_句柄的元数据字段。 如果需要，这使要跟踪的父/子关系的标注驱动程序。

 

 





