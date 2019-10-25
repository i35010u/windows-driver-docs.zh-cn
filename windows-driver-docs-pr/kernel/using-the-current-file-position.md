---
title: 使用当前文件位置
description: 使用当前文件位置
ms.assetid: d342d973-8fff-4d00-a275-114012c17727
keywords:
- 文件 WDK 内核
- 文件对象 WDK 内核
- 对象 WDK 文件对象
- 文件处理 WDK 内核
- 文件 WDK 内核的句柄
- 当前文件的位置 WDK 内核
- 文件位置 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b08b7ac9bc1bdc6d0fcf0aad254dd8b0017eac1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835865"
---
# <a name="using-the-current-file-position"></a>使用当前文件位置





当你创建或打开文件时，可能会导致 i/o 管理器创建与文件句柄关联的当前文件位置指针。 完成此操作后，可以读取数据并将数据写入当前文件位置，i/o 管理器会自动将位置更新为读取或写入的字节数。

默认情况下，i/o 管理器不会保留当前文件位置指针。 此默认值提供了效率，因为正确维护当前文件位置需要 i/o 管理器对文件对象上的每个读写操作进行同步。

若要创建具有关联的当前文件位置指针的句柄，请在*DesiredAccess*参数中指定对[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)、 [**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)或[**ZwOpenFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)的同步访问权限，并将文件\_同步\_IO\_警报或文件\_同步\_IO\_*CreateOptions*或*OpenOptions*参数中的 NONALERT。 请确保不要同时指定文件\_追加\_数据访问权限。

[**ZwReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile)和[**ZwWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile)会自动更新当前的文件位置指针，使其指向的内容不受操作影响的数据的影响。 例如，如果从字节偏移量101开始读取20个字节，则**ZwReadFile**会将当前文件位置更新为121。

您可以通过分别调用[**ZwQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)或[**ZwSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)来检查或更改当前文件位置。 在任一情况下，请将*FileInformationClass*参数设置为**FilePositionInformation**。

 

 




