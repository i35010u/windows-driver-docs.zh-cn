---
title: 客户端呈现概述
description: 客户端呈现概述
keywords:
- 客户端呈现 WDK 打印，关于客户端呈现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff04790f84001c4ff5aa57c45cb7b9afa5a8288
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797723"
---
# <a name="client-side-rendering-overview"></a>客户端呈现概述

[指向和打印](introduction-to-point-and-print.md) 将打印机驱动程序加载到客户端计算机上，就像在以前版本的 Windows 操作系统中一样。 客户端呈现会使打印机驱动程序将打印作业呈现到页面说明语言 (PDL) 打印机使用的 (是 PDL) 格式或 XML 纸张规范 (XPS) 格式（打印机驱动程序使用的格式）。 然后，使用打印后台处理程序中的新功能将原始格式 PDL 发送到打印服务器，以进行排队和打印。

除了将打印作业的处理负载从打印服务器移动到客户端计算机外，客户端呈现还为用户提供了以下优势：

-   消除了驱动程序不匹配问题。

    由于后台打印作业的同一台计算机还呈现 EMF 格式的数据，因此，如果客户端的打印机驱动程序版本与打印服务器上的版本不兼容，则不再存在问题。

-   支持脱机打印。

    最终用户现在可以将打印作业后台处理到远程打印机，即使它们未连接到承载打印机的打印服务器。 使用客户端呈现功能，用户可以在本地后台处理和呈现打印作业。 当客户端计算机可以建立到打印后台处理程序的连接时，呈现的打印作业会自动发送到打印服务器以进行打印。
