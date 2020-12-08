---
title: 一对一 ID 映射
description: 一对一 ID 映射
keywords:
- 映射网络组件 Id
- ID 映射 WDK netmap
- 一对一 ID 映射 WDK 网络
- preupgrade Id WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63d1368800c357f32693633fb13c092daa4969a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825043"
---
# <a name="one-to-one-id-mapping"></a>一对一 ID 映射





**注意**  Microsoft Windows XP (SP1 及更高版本) 、Microsoft Windows Server 2003 和更高版本的操作系统不支持供应商提供的网络升级。

 

Netmap 文件的 **Oem <em>Xxx</em>** 部分中的条目指定了一对一 ID 映射，格式如下：

*preupgrade-ID*  = *postupgrade-ID*

例如：

```cpp
netservice=netservice_2000
```

必须为网络协议、服务和客户端使用一对一 ID 映射。 "一对一 ID 映射" 或 "一对多 ID" 映射可以用于网络适配器。

 

 





