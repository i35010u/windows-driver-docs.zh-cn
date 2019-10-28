---
title: 在驱动程序中使用文件
description: 在驱动程序中使用文件
ms.assetid: 721bf336-1d1d-4677-843d-8af04c6f434d
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- 对象 WDK 文件对象
- 文件处理 WDK 内核
- 文件 WDK 内核的句柄
- 从文件中读取数据
- 将数据写入文件
- 正在读取文件的元数据
- 正在写入文件的元数据
- 驱动程序文件对象 WDK 内核
- 多个文件对象 WDK 内核
- 内核模式驱动程序 WDK，文件
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c7416b6674bf475763624eb45bfba89073fd704
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838358"
---
# <a name="using-files-in-a-driver"></a>在驱动程序中使用文件





Microsoft Windows executive 按*文件对象*（由对象管理器管理的 executive 对象）表示文件。 （目录也由文件对象表示。）

内核模式组件按其对象名称（ **\\DosDevices**连接到文件的完整路径）引用文件。 （在 Microsoft Windows 2000 和更高版本的操作系统上， **\\？** 等效于 **\\DosDevices**。）例如，C：\\WINDOWS\\example .txt 文件的对象名称 **\\DosDevices\\C：\\windows\\example**。 使用对象名称打开文件的句柄。 有关对象名称的详细信息，请参阅[对象名称](object-names.md)。

### <a name="to-use-a-file"></a>使用文件

1.  打开文件的句柄。

    有关详细信息，请参阅[打开文件的句柄](opening-a-handle-to-a-file.md)。

2.  通过调用相应的**Zw*Xxx*文件**例程来执行预期的操作。

    有关详细信息，请参阅[使用文件句柄](using-a-file-handle.md)。

3.  通过调用[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)关闭句柄。

每次打开文件的句柄时，Windows executive 都将创建一个表示该文件的文件对象，并将打开的句柄返回到该对象。 因此，单个文件可以有多个文件对象。 （由于用户模式应用程序可以复制句柄，因此同一文件对象也可以有多个句柄。）关闭文件对象的所有打开句柄后，Windows executive 会删除文件对象。

 

 




