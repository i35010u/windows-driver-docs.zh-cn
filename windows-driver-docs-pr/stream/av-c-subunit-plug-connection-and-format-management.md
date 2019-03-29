---
title: AV/C 子单元插头连接和格式管理
description: AV/C 子单元插头连接和格式管理
ms.assetid: c80641d5-3108-4dbc-91b9-7ed295434b97
keywords:
- 插入连接 WDK AV/C
- 子单元支持 WDK AV/C
- AV/C WDK，即插即用连接
- 对等子单元驱动程序堆栈 WDK AV/C
- KS 固定连接 WDK AV/C
- 将固定连接 WDK AV/C
- 格式 WDK AV/C
- pin 格式 WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0fe524c888c92de7457044f484bd68f570ca6fe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563859"
---
# <a name="avc-subunit-plug-connection-and-format-management"></a>AV/C 子单元插头连接和格式管理





AV/C 对等子单元驱动程序堆栈提供了用于 IEEE 1394 和 AV/C 子单元函数插入连接和格式管理。 内核流式处理 (KS) pin 格式协商和 pin 连接机制转换为插入通过建立的连接*Avc.sys*。 此体系结构的一些关键方面包括：

-   IEEE 1394 和 AV/C 子单元即插即用连接表示为 KS pin DirectShow 筛选器关系图中的新连接。

-   因为只有在没有任何内部的子单元时 KS pin 插入连接功能直接表示 IEEE 1394 串行总线插入 （输入和输出插头）。 当发生这种情况时，没有 IEEE 1394 串行总线即插即用每一个 pin。

-   中的全局唯一标识符 (GUID) 表示 IEEE 1394 串行总线连接。 有关中的 Guid 的详细信息，请参阅[介质和类别](mediums-and-categories.md)。

-   中等 Guid 永久内部 AV/C 单元和子单元连接合成从设备唯一标识符，然后插入地址。

-   有新的 KSDATARANGE 和 KSDATAFORMAT 扩展，以用于 C AV/连接。

媒体和格式结合使用可以帮助确定是否 KS pin 连接表示数据与计算机通过 IEEE 1394 串行总线或设备的内部。

 

 




