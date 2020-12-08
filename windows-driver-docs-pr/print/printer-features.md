---
title: 打印机功能
description: 打印机功能
keywords:
- Unidrv，打印机功能
- GPD 文件 WDK Unidrv，打印机功能
- 打印机功能 WDK Unidrv
- 打印机功能 WDK Unidrv，关于打印机功能
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48ae9cdae52717bbba32c65a2012ac69c6201fd9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807285"
---
# <a name="printer-features"></a>打印机功能





打印机功能可以由 Unidrv 驱动程序控制。 通过在 GPD 文件中列出功能及其特征，你可以通知 Unidrv 驱动程序你的打印机支持该功能。

每个打印机功能可以分配给一个或多个状态，使用 [打印机选项](printer-options.md) 来定义可能的状态。 例如，如果您的打印机同时接受 letter 大小和合法大小的页面，则您的 GPD 文件应指定 PaperSize 功能，同时还应指定字母和法律选项。

所有功能及其关联选项在打印机属性表或与打印机关联的文档属性表中列出。 有关这些属性表的详细信息，请参阅 [Unidrv User Interface](unidrv-user-interface.md)。

本部分介绍 GPD 语言对 [标准功能](standard-features.md) 和 [自定义功能](customized-features.md)的支持。 本节中的其他主题包括 [功能输入格式](feature-entry-format.md)、 [功能属性](feature-attributes.md)和 [功能冲突优先级](feature-conflict-priority.md)。

 

 




