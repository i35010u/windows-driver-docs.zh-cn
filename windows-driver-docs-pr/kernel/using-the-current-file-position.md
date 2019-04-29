---
title: 使用当前文件位置
description: 使用当前文件位置
ms.assetid: d342d973-8fff-4d00-a275-114012c17727
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- WDK 文件对象的对象
- 文件句柄 WDK 内核
- 文件 WDK 内核的句柄
- 当前文件位置 WDK 内核
- 文件位置 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d1fc467973915a96aa87b646c0784561f1423c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372363"
---
# <a name="using-the-current-file-position"></a>使用当前文件位置





当创建或打开文件时，可能会导致 I/O 管理器，以创建一个与文件句柄关联的当前文件位置指针。 完成此操作后，可以读取并将数据写入到当前文件位置，并通过已读取或写入的字节数，I/O 管理器将自动更新位置。

默认情况下，I/O 管理器不维护当前文件位置指针。 此默认值使效率，因为正确维护当前文件位置需要 I/O 管理器以同步每个读取和写入操作对文件对象。

若要创建具有相关当前文件位置的指针，指定同步句柄访问中的右*DesiredAccess*参数[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)，[ **IoCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff548418)，或[ **ZwOpenFile**](https://msdn.microsoft.com/library/windows/hardware/ff567011)，，或者文件\_同步\_IO\_警报或文件\_同步\_IO\_中的警报*CreateOptions*或者*OpenOptions*参数。 确保没有还指定文件\_追加\_数据访问权限。

[**ZwReadFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567072)并[ **ZwWriteFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567121)自动更新当前文件位置的指针，以便它指向刚超出受操作影响的数据。 例如，如果读取 20 个字节处开始的字节偏移量 101 **ZwReadFile**将更新当前文件位置为 121。

可以检查或通过调用来更改当前文件位置[ **ZwQueryInformationFile** ](https://msdn.microsoft.com/library/windows/hardware/ff567052)或[ **ZwSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff567096)，分别。 在任一情况下，设置*FileInformationClass*参数**FilePositionInformation**。

 

 




