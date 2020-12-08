---
title: RAW 数据类型
description: RAW 数据类型
keywords:
- 打印处理器 WDK，数据类型
- 数据类型 WDK 打印处理器
- 原始数据类型 WDK 打印处理器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6d38da3ba4a4b93e02521fd1f47546bed955985
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807069"
---
# <a name="raw-data-type"></a>RAW 数据类型





可以将原始数据发送到打印监视器，而无需进一步处理。 打印处理器只需调用 **WritePrinter**，即可将此数据发送回后台处理程序 (，如 Microsoft Windows SDK 文档) ，有时插入窗体源。 原始数据文件的一个示例是由 *打印机控件语言 (PCL)* 命令组成的。 如果客户端或服务器不支持基于 NT 的操作系统 EMF，或者服务器管理员禁用了 EMF 支持，打印作业将以原始格式从客户端发送到服务器。 在这种情况下，会在将作业发送到服务器之前，在客户端上执行图像渲染。

如果目标打印机支持 Postscript，则可以将 Postscript 命令视为原始数据。 另一方面，Sfmpsprt.dll 打印处理器采用 Postscript 输入并将其解释为非 Postscript 打印机，因此在这种情况下 Postscript 不是原始数据。

有关原始数据类型的详细信息，请参阅 *windows 2000 专业资源工具包* 或 *Windows 2000 服务器资源工具包*。  (这些资源可能在某些语言和国家/地区不可用。 ) 

 

 




