---
title: 指定捆绑成员身份
description: 指定捆绑成员身份
ms.assetid: aa73c7fd-a5c8-4ef5-99fd-229fbcc6b4df
keywords:
- 添加-注册表-每节 WDK 网络，捆绑成员身份
- 捆绑包成员 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdc5913d81588cd5d23f75a0a7a917f23616a88d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207777"
---
# <a name="specifying-bundle-membership"></a>指定捆绑成员身份




> [!NOTE]
> 在 Windows Vista 和更高版本中已弃用捆绑包成员身份。 


一个 INF 文件，用于在物理或虚拟网络适配器 (安装 **网络** 组件) 可以指定这些网络适配器属于相同的适配器包。 请注意，导出虚拟网络适配器的 NDIS 中间驱动程序和筛选器驱动程序包含在 .Net 类中。 NDIS 驱动程序可以使用它安装的适配器来平衡其工作负荷，方法是在适配器捆绑上分配工作负荷。 有关负载平衡的详细信息，请参阅 [负载平衡和故障转移](/previous-versions/windows/hardware/network/ff549197(v=vs.85))。

若要指定适配器属于特定的适配器捆绑，则安装适配器的驱动程序的 INF 文件必须包含 **BundleId** 关键字和不区分大小写的字符串值 (REG \_ SZ) 。 此字符串值标识驱动程序的适配器捆绑包。 注册表使用捆绑标识符信息进行配置。

下面是驱动程序的 INF 文件中的 "*添加注册表" 部分*的示例，该文件将**BundleId**子项添加到**Ndi \\ 参数**键，并为**BundleId**的字符串值 "Bundle1" 提供**ParamDesc** (参数说明) 。

```INF
[a1.params.reg]
HKR, Ndi\params\BundleId, ParamDesc, 0, "Bundle1"
```

 

