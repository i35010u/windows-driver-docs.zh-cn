---
title: COM 端口数据库
description: COM 端口数据库
ms.assetid: c9baf147-6e33-4ed2-b682-c141938eb0da
keywords:
- COM 端口 WDK 串行设备
- 串行设备 WDK，COM 端口
- COM 端口数据库 WDK 串行设备
- COM 端口号 WDK 串行设备
- 端口号 WDK 串行设备
- 释放端口号
- 当前端口号使用情况 WDK 串行设备
- 大小 WDK COM 端口数据库
- 调整 COM 端口数据库的大小
- 数据库 WDK COM 端口数据库
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76ac4e29bce16f019d1a8f22b167b200770373e6
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716670"
---
# <a name="com-port-database"></a>COM 端口数据库

系统提供的 COM 端口数据库仲裁系统上安装的 [com](configuration-of-com-ports.md) 端口使用 com 端口号。 Microsoft Windows 提供此组件以便于安装 COM 端口，尤其是确保每个端口号至少分配到一个端口。 组件包含数据库和库，其中包含安装软件调用以访问数据库的函数。 适用于 COM 端口的所有系统提供的安装程序均使用 COM 端口数据库来获取 COM 端口号。 尽管不是即插即用要求，但所有供应商提供的安装程序还应该使用 COM 端口数据库来获取 COM 端口号。

有关支持 COM 端口数据库的例程的信息，请参阅 COMPort 数据库支持例程：

[ComDBClaimNextFreePort](/windows/win32/api/msports/nf-msports-comdbclaimnextfreeport)

[ComDBClaimPort](/windows/win32/api/msports/nf-msports-comdbclaimport)

[ComDBClose](/windows/win32/api/msports/nf-msports-comdbclose)

[ComDBGetCurrentPortUsage](/windows/win32/api/msports/nf-msports-comdbgetcurrentportusage)

[ComDBOpen](/windows/win32/api/msports/nf-msports-comdbopen)

[ComDBReleasePort](/windows/win32/api/msports/nf-msports-comdbreleaseport)

[ComDBResizeDatabase](/windows/win32/api/msports/nf-msports-comdbresizedatabase)

另请参阅以下例程：

[SerialDisplayAdvancedSettings](/windows/win32/api/msports/nf-msports-serialdisplayadvancedsettings)，它是系统提供的例程，用于安装 COM 端口的高级属性页

[PPORT_ADVANCED_DIALOG](/previous-versions/windows/hardware/drivers/ff546956(v=vs.85))类型的例程，该例程提供由**SerialDisplayAdvancedSettings**调用的可选供应商提供的对话框

若要在安装程序中调用这些例程，请将安装程序链接到 *msports*，后者随 Windows 驱动程序工具包一起提供 (WDK) 。

## <a name="structure-of-the-com-port-database"></a>COM 端口数据库的结构

COM 端口数据库由元素数组组成，每个元素指示 COM 端口号是否正在使用。 第一个数组元素对应于 COM1，第二个数组元素对应于 COM2，依此类推。 但是，数据库不包含有关分配有给定端口号的设备的任何信息。 数据库的大小等于数据库当前仲裁的端口号的数量。 数据库仲裁的最小端口号数为 COMDB \_ 最小 \_ 端口 \_ 仲裁，最大仲裁数为 COMDB \_ MAX \_ 端口 \_ 仲裁。 可以使用 [**ComDBResizeDatabase**](/windows/win32/api/msports/nf-msports-comdbresizedatabase) 例程提高数据库的大小。

## <a name="opening-and-closing-the-com-port-database"></a>打开和关闭 COM 端口数据库

在使用 COM 端口数据库之前，客户端必须通过调用 [**ComDBOpen**](/windows/win32/api/msports/nf-msports-comdbopen) 例程打开数据库以获取数据库的句柄。 数据库在任何连续数据库访问过程中由互斥保护。 但是，数据库无法处于独占使用状态，并且其状态可以在对数据库的不同访问之间动态变化。

## <a name="determining-the-current-usage-of-com-port-numbers"></a>确定 COM 端口号的当前使用情况

打开 COM 端口数据库后，客户端可以通过调用 [**ComDBGetCurrentPortUsage**](/windows/win32/api/msports/nf-msports-comdbgetcurrentportusage) 例程来确定哪些 COM 端口号已被使用。

客户端通常会执行以下任务：

1. 调用例程来确定数据库中当前正在仲裁的端口号数量。

2. 第二次调用例程，返回调用方分配的位数组或字节数组中端口号使用情况的相关信息，其中每个位或 byte 指定了相应的端口号是否正在使用中。

如果数据库中的所有端口号都正在使用，或者当前没有合适的端口号可用，则客户端可以调整数据库的大小。 有关详细信息，请参阅调整 COM 端口数据库的大小。

## <a name="obtaining-and-releasing-a-com-port-number"></a>获取和释放 COM 端口号

客户端可以通过调用以下例程之一来获取 COM 端口号：

- [**ComDBClaimNextFreePort**](/windows/win32/api/msports/nf-msports-comdbclaimnextfreeport)，用于声明最低可用的端口号。

- [**ComDBClaimPort**](/windows/win32/api/msports/nf-msports-comdbclaimport)，它尝试声明特定的端口号。

在 COM 端口数据库中*声明*一个 com 端口号会将端口号记录为 "正在使用"。

客户端通过调用 [**ComDBReleasePort**](/windows/win32/api/msports/nf-msports-comdbreleaseport) 例程来释放端口号。

## <a name="resizing-the-com-port-database"></a>调整 COM 端口数据库的大小

客户端可以通过调用 [**ComDBResizeDatabase**](/windows/win32/api/msports/nf-msports-comdbresizedatabase) 例程调整 COM 端口数据库的大小。 客户端只能通过1024的整数倍数增加数据库的大小。 数据库的最大大小为 COMDB \_ MAX \_ 端口 \_ 仲裁。