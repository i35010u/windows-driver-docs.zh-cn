---
title: 创建 GDL 配置相关的数据
description: 创建 GDL 配置相关的数据
ms.assetid: 5b00903c-a637-4f83-96b8-92fe850d309e
keywords:
- GDL WDK 配置
- 配置 WDK GDL，创建依赖于配置的数据
- 创建依赖于配置的数据 WDK GDL
- GDL WDK，组织数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9fd2f7d1ffc03a87164a47776dc77830b6db3d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365573"
---
# <a name="creating-gdl-configuration-dependent-data"></a>创建 GDL 配置相关的数据


GDL 语言，可定义其值取决于一个或多个参数的数据。 GDL 客户端不需要知道数据的参数集的依赖性或甚至不知道的数据取决于参数。 GDL 客户端需要知道仅要分配给每个参数的值，然后 GDL 将构造快照，以便所有数据都适用于指定的参数值。

配置依赖于数据 (CDD) 是依赖于一个或多个参数的数据。 需要访问同一组下不同条件或配置的数据的客户端将依赖于配置的数据的理想的使用者。 例如，在用户指定的位置和日期始终显示天气情况的应用程序显示相同的信息 （例如，每日信用、 每日最高价和最温度和平均天空条件）。 位置和日期将成为用于构造用于获取数据的快照的配置的参数。 GDL 轻松，可将数据组织到依赖于配置的窗体。

若要使用 GDL 将数据组织到依赖于配置的窗体，请按照这两个步骤操作：

1.  定义的参数。

2.  添加到的数据的依赖项。

创建用于描述数据的 GDL 文件后，客户端需要指定所需的配置和请求快照。

下面的主题介绍的步骤来创建和组织依赖于配置的数据：

[定义依赖于配置的数据参数](defining-the-configuration-dependent-data-parameters.md)

[将依赖项添加到依赖于配置的数据](adding-dependencies-to-the-configuration-dependent-data.md)

[创建 GDL 快照](creating-gdl-snapshots.md)

 

 




