---
title: 一对一 ID 映射
description: 一对一 ID 映射
ms.assetid: fd9a98a4-5796-4d39-a83b-427b320b32da
keywords:
- 映射网络组件 Id
- ID 映射 WDK netmap.inf
- 一对一 ID 映射 WDK 网络
- 升级前 Id WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4b8d21a386c3af1bbca48b3f51cc2c33531a395
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384226"
---
# <a name="one-to-one-id-mapping"></a>一对一 ID 映射





**请注意**  供应商提供网络升级不支持在 Microsoft Windows XP (SP1 和更高版本)，Microsoft Windows Server 2003 和更高版本操作系统。

 

中的条目**Oem * Xxx*** 部分中的指定 ID 的一对一映射的 netmap.inf 文件采用以下格式：

*preupgrade-ID* = *postupgrade-ID*

例如：

```cpp
netservice=netservice_2000
```

ID 的一对一映射必须用于网络协议、 服务和客户端。 ID 的一对一映射或一个多 ID 映射可用于网络适配器。

 

 





