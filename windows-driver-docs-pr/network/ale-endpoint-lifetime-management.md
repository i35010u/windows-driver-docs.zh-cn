---
title: ALE 终结点生存期管理
description: ALE 终结点生存期管理
ms.assetid: cbf54062-4ced-4cf6-babf-e9e4e1ddf302
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de81b2413b85e23d8bed928ea1cced6c5bfd541f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835388"
---
# <a name="ale-endpoint-lifetime-management"></a>ALE 终结点生存期管理


支持应用程序层强制（ALE）的标注驱动程序可能需要分配资源来处理指示。 本主题介绍如何将标注驱动程序配置为在关联的终结点关闭时释放此类资源。 在 windows 7 和更高版本的 Windows 中，会支持 ALE 终结点生存期。

若要管理与 ALE 终结点关联的资源，标注驱动程序可在以下层注册：

-   FWPS\_层\_ALE\_资源\_RELEASE\_V4 （FWPM\_层\_ALE\_资源\_RELEASE\_V4）

-   FWPS\_层\_ALE\_资源\_RELEASE\_V6 （FWPM\_层\_ALE\_资源\_RELEASE\_V6）

-   FWPS\_层\_ALE\_终结点\_关闭\_V4 （FWPM\_层\_ALE\_终结点\_关闭\_V4）

-   FWPS\_层\_ALE\_终结点\_关闭\_V6 （FWPM\_层\_ALE\_终结点\_的 V6）

为每个指示指定了 ale 资源释放层（例如，FWPS\_层\_ALE\_资源\_分配\_V4）。 为了确保标注驱动程序可以将发布层与分配层相匹配，FWPS\_元数据\_字段\_传输\_终结\_点在两个层上均提供，并为每个终结点分配唯一柄.

根据终结点的类型，将以不同的方式调用 ALE 终结点闭层。 对于 TCP 连接，会为每个 ALE 授权连接层（例如，FWPS\_层\_ALE\_authentication\_连接\_V4）或 ALE 授权接收方（例如 FWPS\_层）指定 ALE 终结点闭包。\_ALE\_AUTH\_接收\_接受\_V4）指示。 与 ALE 资源发布指示一样，引擎为每个终结点分配一个唯一的句柄，并将其传递到 FWPS\_元数据\_字段\_传输\_终结点\_处理元数据字段。 对于非 TCP 终结点，将为每个终结点调用 ALE 终结点关闭层，而与套接字通信的唯一远程对等机的数量无关。 还会为每个 TCP 侦听套接字调用 ALE 终结点关闭层。

为 ALE 终结点闭层注册的标注可以挂起分类。 这使标注能够在关闭终结点之前 reinject 排队等待异步处理的任何数据包。 若要挂起分类，标注驱动程序必须先调用[**FwpsPendClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0) ，然后在处理完成时调用[**FwpsCompleteClassify0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteclassify0) 。

如果适用，引擎将在 FWPS\_元数据 "\_字段\_父\_终结点\_处理元数据" 字段中为父终结点指定唯一的句柄。 这使标注驱动程序能够跟踪父/子关系（如果需要）。

 

 





