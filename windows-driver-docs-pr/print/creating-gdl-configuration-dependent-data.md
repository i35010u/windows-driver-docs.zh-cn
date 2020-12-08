---
title: 创建 GDL 配置相关的数据
description: 创建 GDL 配置相关的数据
keywords:
- GDL WDK，配置
- 配置 WDK GDL，创建依赖于配置的数据
- 创建依赖于配置的数据 WDK GDL
- GDL WDK，组织数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e185dad5c3b59c723b80d3bf903b87f6fcf9c65
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797467"
---
# <a name="creating-gdl-configuration-dependent-data"></a>创建 GDL 配置相关的数据


GDL 语言使你能够定义其值依赖于一个或多个参数的数据。 GDL 客户端无需知道数据在参数上的依赖关系，甚至知道数据依赖于参数。 GDL 客户端需要仅知道要分配给每个参数的值，然后 GDL 将构造快照，以便所有数据都适用于指定的参数值。

依赖于配置的数据 (CDD) 是依赖于一个或多个参数的数据。 需要在不同条件或配置下访问同一组数据的客户端是依赖于配置的数据的理想使用者。 例如，在用户指定的位置和日期显示天气条件的应用程序始终显示相同的信息 (例如，每日降雨量、每日高温和低温度，以及平均天空条件) 。 位置和日期将成为用来构造用于获取数据快照的配置的参数。 GDL 使你能够轻松地将数据组织成依赖于配置的形式。

若要使用 GDL 将数据组织为依赖于配置的表单，请遵循以下两个步骤：

1.  定义参数。

2.  将依赖项添加到数据。

在创建了说明数据的 GDL 文件之后，客户端需要指定所需的配置并请求一个快照。

以下主题介绍了创建和组织依赖于配置的数据的步骤：

[定义配置相关的数据参数](defining-the-configuration-dependent-data-parameters.md)

[将依赖项添加到配置相关的数据](adding-dependencies-to-the-configuration-dependent-data.md)

[创建 GDL 快照](creating-gdl-snapshots.md)

 

 




