---
title: 使用当前文件位置
description: 使用当前文件位置
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
ms.openlocfilehash: 043f7c627982943659aa70b1050a277d9dc1cb8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803755"
---
# <a name="using-the-current-file-position"></a>使用当前文件位置





当你创建或打开文件时，可能会导致 i/o 管理器创建与文件句柄关联的当前文件位置指针。 完成此操作后，可以读取数据并将数据写入当前文件位置，i/o 管理器会自动将位置更新为读取或写入的字节数。

默认情况下，i/o 管理器不会保留当前文件位置指针。 此默认值提供了效率，因为正确维护当前文件位置需要 i/o 管理器对文件对象上的每个读写操作进行同步。

若要创建具有关联的当前文件位置指针的句柄，请在 *DesiredAccess* 参数中指定对 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)、 [**IoCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)或 [**ZwOpenFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntopenfile)的同步访问权限，并在 \_ \_ \_ \_ \_ \_ *NONALERT* 或 *CreateOptions* 参数中指定 "同步 io 警报" 或 "文件同步 io OpenOptions"。 请确保不要同时指定文件 \_ 追加 \_ 数据访问权限。

[**ZwReadFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntreadfile) 和 [**ZwWriteFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntwritefile) 会自动更新当前的文件位置指针，使其指向的内容不受操作影响的数据的影响。 例如，如果从字节偏移量101开始读取20个字节，则 **ZwReadFile** 会将当前文件位置更新为121。

您可以通过分别调用 [**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile) 或 [**ZwSetInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)来检查或更改当前文件位置。 在任一情况下，请将 *FileInformationClass* 参数设置为 **FilePositionInformation**。

 

