---
title: IRP 日志记录
description: Driver Verifier 的 IRP 日志记录功能监视的 Irp 的驱动程序的使用，并使 IRP 使用情况的记录。 此记录存储为 WMI 信息。
ms.assetid: 368356df-7fa7-4555-b5cf-59c26d70075e
keywords:
- IRP 日志记录功能 WDK Driver Verifier
- DC2WMIParser 工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1e3cdc8267cf6727e58c6891ecdbe30f2b52114
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547145"
---
# <a name="irp-logging"></a>IRP 日志记录


Driver Verifier 的 IRP 日志记录功能监视的 Irp 的驱动程序的使用，并使 IRP 使用情况的记录。 此记录存储为 WMI 信息。

## <span id="ddk_irp_logging_tools"></span><span id="DDK_IRP_LOGGING_TOOLS"></span>


Windows Driver Kit (WDK) 包括工具 DC2WMIParser (dc2wmiparser.exe)，可以将此 WMI 记录转换为文本文件。

此驱动程序验证程序选项才可用在 Windows Server 2003 及更高版本。

### <a name="span-idthewmirecordspanspan-idthewmirecordspanthe-wmi-record"></a><span id="the_wmi_record"></span><span id="THE_WMI_RECORD"></span>WMI 记录

WMI 记录不会超过 20 种 Irp 为每个设备。 一旦记录第 21 个 IRP，将替换为第一 IRP 条记录。 因此，如果记录列出了 20 个 Irp，这些始终是最新的 20，但没有办法知道以下哪些是最新。

由于 WMI 记录存储在内存中，将重新启动计算机时清除。 因此，使用 DC2WMIParser 将此信息保存到一个文件。

如果您使用 **/t**选项，DC2WMIParser 将连续运行指定的持续时间。 在这种情况下，该记录可以包含超过 20 种 Irp，每个设备 (最多 20 个 Irp 中每个采样期间)。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的 IRP 日志记录功能。

若要激活 IRP 日志记录功能，您必须激活[I/O 验证](i-o-verification.md)。

-   **在命令行**

    在命令行中，由表示 IRP 日志记录选项**0x400** (位 10)。

    若要激活 IRP 日志记录，请使用 0x410 标志值或将 0x410 添加到标志值。 此值将激活[I/O 验证](i-o-verification.md) (0x10) 和 IRP 日志记录 (0x400)。 例如：

    ```
    verifier /flags 0x410 /driver MyDriver.sys
    ```

    在下一次启动后，该功能将处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，您可以还激活和停用而无需重启计算机，通过添加的 IRP 日志记录 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x410 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

-   **使用驱动程序验证程序管理器**
    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择 （选中） **IRP 日志记录**并[I/O 验证](i-o-verification.md)。

### <a name="span-iddc2wmiparserspanspan-iddc2wmiparserspandc2wmiparser"></a><span id="dc2wmiparser"></span><span id="DC2WMIPARSER"></span>DC2WMIParser

DC2WMIParser 是一种工具，收集由驱动程序验证程序创建的 WMI IRP 记录，并将此日志转换为文本文件。

DC2WMIParser 语法如下所示：

```
dc2wmiparser [/f File] [/t Time]
```

参数具有以下含义：

<span id="_________fFile"></span><span id="_________ffile"></span><span id="_________FFILE"></span> **/f***File*  
指定完整路径和要写入的日志文件的文件名。 将相对于当前目录中提取的相对路径。 如果省略此属性，将使用当前目录中的文件名称 dc2verifier.act。

<span id="_tTime"></span><span id="_ttime"></span><span id="_TTIME"></span>**/t***Time*  
指定的时间，以分钟为单位 DC2WMIParser 将继续运行。 如果*时间*等于零，DC2WMIParser 将记录已存储驱动程序验证程序的所有 WMI IRP 信息，然后退出。 如果*时间*设置为正值，DC2WMIParser 将继续以运行适用于指定长度的时间，存储的新信息到达时。 默认值为 0。

### <a name="span-idformatofdc2wmiparserlogfilesspanspan-idformatofdc2wmiparserlogfilesspanformat-of-dc2wmiparser-log-files"></a><span id="format_of_dc2wmiparser_log_files"></span><span id="FORMAT_OF_DC2WMIPARSER_LOG_FILES"></span>DC2WMIParser 日志文件的格式

DC2WMIParser 生成的文件是 ASCII 文本文件。

此文件的第一行包含表示文件中记录的设备数的十进制数。

在第一行，后面文件划分部分;每个部分介绍了一台设备。

对于每个设备的格式为：

-   **在单独的行：** 设备名称。

-   **在单独的行：** 指定多少设备类型和函数针对此设备的十进制数字。

-   **在为每个设备类型和函数的同一行：** 三个十六进制数字，由逗号分隔。 这些表示设备类型，并将此记录中记录的最低和最高函数。

-   **中的行，以便每个设备类型和函数的一个组：**
    -   十进制数字，指定当前的设备类型 Ioctl 的计数与单个行。
    -   每个 IOCTL 的一个行。 每行包含六个由逗号分隔的十六进制数字。 这些名称指定的设备类型、 函数、 方法、 访问、 输入缓冲区的长度和输出缓冲区的长度。

下面是示例 DC2WMIParser 日志文件。 在实际文件中将不会有任何空格、 注释或空白行，但它们已添加到此示例，以使其更清晰。

```
2           There are two devices described by this log file.

The first device begins here:

  DP(1)0x7e00-0x21dbda400+3   Device name of the first device
  2                           Number of device type IOCTLs targeted at this device

    7,12,12                     First targeted device: device type 7, low function 12, high function 12
    2d,420,420                  Second targeted device: device type 2d, low function 420, high function 420

    1                           Number of IOCTLs for first targeted  device (type 7)
      7,12,0,0,90,0               Device type 7, function 12, method 0, access 0, inbuflen 90, outbuflen 0
    1                           Number of IOCTLs for second targeted device (type 2d)
      2d,420,0,0,c,0              Device type 2d, function 420, method 0, access 0, inbuflen c, outbuflen 0

The second device begins here:

  DP(1)0x7e00-0x21dbda400+2   Device name of the second device
  2                           Number of device type IOCTLs targeted at this device

    7,12,12                     First targeted device: device type 7, low function 12, high function 12
    2d,420,420                  Second targeted device: device type 2d, low function 420, high function 420


    1                           Number of IOCTLs for first targeted  device (type 7)
      7,12,0,0,90,0               Device type 7, function 12, method 0, access 0, inbuflen 90, outbuflen 0
    1                           Number of IOCTLs for second targeted device (type 2d)
      2d,420,0,0,c,0              Device type 2d, function 420, method 0, access 0, inbuflen c, outbuflen 0
```

 

 





