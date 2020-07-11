---
title: 使用扩展 INF 文件模板
description: 介绍如何使用扩展 INF 模板
ms.topic: article
ms.localizationpriority: medium
ms.date: 06/12/2020
ms.openlocfilehash: 7a15d1b449fc3c7a2238662b4ac094b2ebc700f7
ms.sourcegitcommit: 5148f4ff682a2d9cdf5eafdb76e13400331f5660
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2020
ms.locfileid: "86273189"
---
# <a name="using-an-extension-inf-file-template"></a>使用扩展 INF 文件模板

本页介绍如何使用扩展 INF 模板来改善可扩展性。

扩展 INF 模板是一个扩展 INF，其中条目注释掉了设备制造商 (IHV) 在单独的驱动程序包中发布。 通常情况下，IHV 会将可选功能从基本 INF 中分离出来，并将其放在扩展 INF 模板中。 在模板中，IHV 提供了注释，指示系统生成器 (OEM) 可以取消注释和更改的项，以及可取消注释但不应更改的项。  然后，OEM 使用模板作为创建扩展 INF 的起点。

若要基于模板创建扩展 INF，请遵循[创建扩展 inf](using-an-extension-inf-file.md#creating-an-extension-inf)中的指南，并参考该页面底部的示例。

若要提交基于模板的新扩展 INF，请使用[DUA 进程](https://docs.microsoft.com/windows-hardware/test/hlk/user/create-a-driver-only-update-package)。

> [!NOTE]
> 如果 OEM 使用 DUA 进程来修改 IHV 提供的基本 INF，则基本 INF 的所有权将转移到 OEM。 相反，OEM 应联系 IHV，并请求将适当的扩展性添加到基本 INF，或 IHV 提供扩展 INF 模板。

IHV 还可以使用扩展 INF 模板将可选功能添加到已发布的驱动程序包。 通过发布模板而不是更新基本 INF，IHV 有助于确保现有扩展 Inf 继续工作。 以下顺序说明了这种情况的工作方式：

1. IHV 将新的可选值添加到扩展 INF 模板，而不是基本 INF。
2. IHV 将代码添加到基本驱动程序，以检查是否存在新的注册表值：
    * 如果更新的基本驱动程序找到新值，则它将使用新功能。
    * 否则，它使用以前的功能。
3. OEM 使用扩展 INF 模板来创建新的扩展 INF，以设置新的值。

否则，IHV 决定更新基本 INF，请遵循[使用扩展 INF 文件](using-an-extension-inf-file.md#backward-compatibility)中所述的指导原则。

## <a name="related-topics"></a>相关主题

* [使用扩展 INF 文件](using-an-extension-inf-file.md)
* [在合作伙伴中心使用扩展 INF](../dashboard/submit-dashboard-extension-inf-files.md)
