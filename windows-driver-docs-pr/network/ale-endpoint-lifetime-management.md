---
title: ALE 终结点生存期管理
description: ALE 终结点生存期管理
ms.assetid: cbf54062-4ced-4cf6-babf-e9e4e1ddf302
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10ab06aed792bd3e66663bb703aed6fc959767cc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212975"
---
# <a name="ale-endpoint-lifetime-management"></a>ALE 终结点生存期管理


支持应用程序层强制 (ALE) 的标注驱动程序可能需要分配资源来处理指示。 本主题介绍如何将标注驱动程序配置为在关联的终结点关闭时释放此类资源。 在 windows 7 和更高版本的 Windows 中，会支持 ALE 终结点生存期。

若要管理与 ALE 终结点关联的资源，标注驱动程序可在以下层注册：

-   FWPS \_ 层 \_ ale \_ 资源 \_ 释放 \_ v4 (FWPM \_ 层 \_ ale \_ 资源 \_ 释放 \_ v4) 

-   FWPS \_ 层 \_ ale \_ 资源 \_ 发布 \_ v6 (FWPM \_ 层 \_ ale \_ 资源 \_ 释放 \_ v6) 

-   FWPS \_ 层 \_ ale \_ 终结点 \_ 关闭 \_ v4 (FWPM \_ 层 \_ ale \_ 终结点 \_ 关闭 \_ v4) 

-   FWPS \_ 层 \_ ale \_ 终结点 \_ 关闭 \_ v6 (FWPM \_ 层 \_ ale \_ 终结点 \_ 关闭 \_ v6) 

为每个指示指定了 ale 资源释放层，每个指示在相应的 ALE 资源分配层 (例如，FWPS \_ 层 \_ ALE \_ 资源 \_ 分配 \_ V4) 。 为了确保标注驱动程序可以将发布层与分配层相匹配，FWPS \_ 元数据 \_ 字段 \_ 传输 \_ 终结点 \_ 处理元数据字段是在这两个层上提供的，每个终结点都分配有一个唯一的句柄。

根据终结点的类型，将以不同的方式调用 ALE 终结点闭层。 对于 TCP 连接，将为每个 ALE 授权连接层指定 ALE 终结点闭包 (例如 FWPS \_ 层 \_ ale \_ 身份验证 \_ 连接 \_ V4) 或 ALE 授权接收接受层 (例如，FWPS \_ 层 \_ ale \_ 身份验证 \_ 接收 \_ 接受 \_ V4) 指示。 与 ALE 资源发布指示一样，引擎为每个终结点分配一个唯一的句柄，并将其传递到 FWPS \_ 元数据 \_ 字段 \_ 传输 \_ 终结点 \_ 处理元数据字段。 对于非 TCP 终结点，将为每个终结点调用 ALE 终结点关闭层，而与套接字通信的唯一远程对等机的数量无关。 还会为每个 TCP 侦听套接字调用 ALE 终结点关闭层。

为 ALE 终结点闭层注册的标注可以挂起分类。 这使标注能够在关闭终结点之前 reinject 排队等待异步处理的任何数据包。 若要挂起分类，标注驱动程序必须先调用 [**FwpsPendClassify0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendclassify0) ，然后在处理完成时调用 [**FwpsCompleteClassify0**](/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpscompleteclassify0) 。

如果适用，引擎将在 "FWPS \_ 元数据" \_ 字段 " \_ 父终结点" " \_ \_ 元数据" 字段中为父终结点指定唯一的句柄。 这使标注驱动程序能够跟踪父/子关系（如果需要）。

 

