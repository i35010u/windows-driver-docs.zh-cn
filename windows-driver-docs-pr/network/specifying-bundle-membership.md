---
title: 指定捆绑成员身份
description: 指定捆绑成员身份
ms.assetid: aa73c7fd-a5c8-4ef5-99fd-229fbcc6b4df
keywords:
- 添加注册表部分 WDK 网络，捆绑包成员身份
- 捆绑包成员资格 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86d05b309142d200f4cee8f9ba7fcfcb259e6512
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342579"
---
# <a name="specifying-bundle-membership"></a>指定捆绑成员身份




> [!NOTE]
> 在 Windows Vista 及更高版本已弃用捆绑包成员身份。 


安装一个 INF 文件**Net**组件 （物理或虚拟网络适配器） 可以指定这些网络适配器属于适配器在同一个包。 请注意，NDIS 中间层驱动程序筛选器驱动程序，它将导出的虚拟网络适配器，包括 Net 类中。 NDIS 驱动程序可以使用它安装为平衡其工作负荷，方法是将工作负荷分布在适配器的绑定的适配器。 有关负载平衡的详细信息，请参阅[负载平衡和故障转移](https://msdn.microsoft.com/library/windows/hardware/ff549197)。

若要指定适配器属于一组特定的适配器，适配器将安装该驱动程序的 INF 文件必须包含**BundleId**关键字和不区分大小写的字符串值 (REG\_SZ)。 此字符串值标识适配器的驱动程序的捆绑的包。 注册表使用捆绑包标识符信息进行配置。

以下是一种*添加注册表部分*中添加的驱动程序的 INF 文件**BundleId**到子项**Ndi\\params**密钥并提供**ParamDesc** （参数说明） 的**BundleId** "Bundle1"字符串值。

```INF
[a1.params.reg]
HKR, Ndi\params\BundleId, ParamDesc, 0, "Bundle1"
```

 

 





