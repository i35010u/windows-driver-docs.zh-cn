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
ms.openlocfilehash: c3ae511843de7f97aeb74653250b7b15b35128e8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358183"
---
# <a name="using-the-current-file-position"></a>使用当前文件位置





当创建或打开文件时，可能会导致 I/O 管理器，以创建一个与文件句柄关联的当前文件位置指针。 完成此操作后，可以读取并将数据写入到当前文件位置，并通过已读取或写入的字节数，I/O 管理器将自动更新位置。

默认情况下，I/O 管理器不维护当前文件位置指针。 此默认值使效率，因为正确维护当前文件位置需要 I/O 管理器以同步每个读取和写入操作对文件对象。

若要创建具有相关当前文件位置的指针，指定同步句柄访问中的右*DesiredAccess*参数[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)，[ **IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)，或[ **ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntopenfile)，，或者文件\_同步\_IO\_警报或文件\_同步\_IO\_中的警报*CreateOptions*或者*OpenOptions*参数。 确保没有还指定文件\_追加\_数据访问权限。

[**ZwReadFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntreadfile)并[ **ZwWriteFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntwritefile)自动更新当前文件位置的指针，以便它指向刚超出受操作影响的数据。 例如，如果读取 20 个字节处开始的字节偏移量 101 **ZwReadFile**将更新当前文件位置为 121。

可以检查或通过调用来更改当前文件位置[ **ZwQueryInformationFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntqueryinformationfile)或[ **ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile)，分别。 在任一情况下，设置*FileInformationClass*参数**FilePositionInformation**。

 

 




