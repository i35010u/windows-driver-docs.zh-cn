---
title: 用户界面插件简介
description: 用户界面插件简介
ms.assetid: 7f01bd14-bcc5-4c26-a9b8-a12aa1ffe242
keywords:
- 用户界面插件 WDK 打印，有关用户界面插件
- 打印、 有关用户界面插件的 UI 插件 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ae0feca471cbaab42b958a8ae98e65918859654
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376919"
---
# <a name="introduction-to-user-interface-plug-ins"></a>用户界面插件简介





当将对新打印机设备的支持添加到任一[Microsoft 通用打印机驱动程序](microsoft-universal-printer-driver.md)(Unidrv) 或[Microsoft PostScript 的打印机驱动程序](microsoft-postscript-printer-driver.md)(Pscript)，你可以自定义驱动程序的用户通过修改打印机属性表或您的打印机的文档属性表的接口。

通过提供用户模式 DLL 来完成此自定义。 此 DLL 被称为*插件的用户界面*，或仅*UI 插件*。

UI 插件可以通过添加、 删除或替换的属性表中的选项来修改打印机属性表**设备设置**页。 它还可以添加一个新页面。 同样，该插件可以修改文档属性表通过添加、 删除或替换的属性表中的选项**布局**，**纸张/质量**，和**高级**页，也可以添加一个新页面。

如果使用的从 Windows Vista Unidrv，可以实现[ **IPrintOemUI2::HideStandardUI** ](https://msdn.microsoft.com/library/windows/hardware/ff554142)中要隐藏所有打印机配置属性的插件方法页标准驱动程序提供了。 如果您想要提供完全自定义打印机配置用户界面为您的打印机，可以使用此方法。

**重要**   Windows 帮助 (WinHlp32.exe) 是使用户能够查看.hlp 文件的应用程序。 从 Windows Vista 开始，Windows 帮助应用程序不包括 Windows 操作系统的一部分。 软件开发人员开发的应用程序依赖于.hlp 文件应转换为备用帮助格式，如.chm、.hxs、.html 或.xml 文件及其文件。 有关详细信息，请参阅[Windows 帮助程序 (WinHlp32.exe) 不再包含在 Windows](https://go.microsoft.com/fwlink/p/?linkid=80917)知识库文章。

 

[打印机接口 DLL](printer-interface-dll.md)调用 UI 插件 Unidrv 或 Pscript，与一组 COM 接口。 Dll 实现使用 CPSUI 和插件的用户界面的打印机接口间接与交互 CPSUI 通过驱动程序的打印机接口 DLL。 因此，应阅读[CPSUI](common-property-sheet-user-interface.md)部分之后再开发插件的 UI。

还可以修改打印机驱动程序的用户界面，UI 插件可以执行其他操作，如处理某些打印机事件和报告支持的功能。 有关详细信息，请参阅[自定义其他打印机接口操作](customizing-other-printer-interface-operations.md)。

 

 




